# Fresh Eyes — Getting Started with JSON++ / jq++

A 5-minute orientation so you can start the task. If anything here doesn't work,
that itself is useful feedback — note it in the questionnaire.

---

## 1. Prerequisites

You need three things on your `PATH`:

| Tool | Check | If missing |
|---|---|---|
| Go 1.24+ | `go version` | https://go.dev/dl/ |
| `jq` | `jq --version` | `brew install jq` / `apt install jq` |
| `ruby` | `ruby --version` | preinstalled on macOS; `apt install ruby` on Linux |

## 2. Get the tools (`jq++` and `yq++`)

```sh
git clone https://github.com/dakusui/jqplusplus.git
cd jqplusplus
go build -o bin/jq++ ./cmd/jqplusplus          # builds bin/jq++
export PATH="$PWD/bin:$PWD/tools/bin:$PATH"     # jq++ (bin), yq++ (tools/bin)
```

> **Already have `jq++` installed?** Please still run the steps above. `yq++` is a
> separate script that ships with the `jqplusplus` repo (not with `jq++`), so a prior
> `jq++` install won't include it. Running these steps puts `yq++` on your PATH and
> gives you a `jq++` verified for this task (v0.0.38 or later); the `export PATH` line
> puts this build ahead of any older `jq++` you may already have.

Verify:

```sh
jq++ --version                # e.g. jq++ version v0.0.38
command -v yq++               # prints the yq++ path if it's on PATH
```

- **`yq++`** turns your `.yaml++` sources into YAML — it's the tool you'll use for the task.
- **`jq++`** is the engine underneath; you'll also call it directly in the verify step (§4).[^tools]

## 3. JSON++ in 5 minutes

JSON++ is ordinary YAML/JSON plus a few reserved keys. The ones you need:

| Construct | What it does |
|---|---|
| `$extends: [base.yaml++]` | Inherit from one or more base files. Later fields override earlier ones; the current file wins over its parents. |
| *(object fields)* | **Deep-merged** — a child object merges into the parent object key by key. |
| *(array fields)* | **Replaced, not merged** — if the child sets an array field, its array replaces the parent's entirely. |
| `$extends` on a list item | You can inherit a base for a single array element (e.g. one step) and override just the fields that differ. |
| `eval:string:EXPR` | A `jq` expression evaluated *after* inheritance resolves (e.g. `refexpr(".foo")` reads another field). |
| `_name:` (underscore prefix) | A private "holder" field for use by expressions; **stripped from the output**.[^holder] |

> **Want more depth?** The full JSON++ / jq++ reference is at
> <https://dakusui.github.io/jqplusplus/>. You don't need it for this task, but it's
> handy if you get curious — or if you're using an AI assistant, which can read the
> full docs to help you.

### A tiny worked example

`greeting.yaml++`:
```yaml
greeting: Hello
```

`hello.yaml++`:
```yaml
$extends: [greeting.yaml++]
name: Mark
```

Run it:
```sh
yq++ hello.yaml++
```
```yaml
greeting: Hello
name: Mark
```

The child inherited `greeting` and added `name`. That's the whole idea — factor
what repeats into a base, and let each file keep only what's different.

## 4. The task workflow

1. **Author** your JSON++ sources in a `work/` folder: put shared structure in base
   files, and make each leaf `$extends` them, keeping only what differs. Leave
   `starter-corpus/` unchanged — you'll verify against it.
2. **Point `jq++` at your shared bases** so `$extends` can find them:
   ```sh
   export JF_PATH=path/to/your/shared
   ```
3. **Generate** YAML for a leaf:
   ```sh
   yq++ your-leaf.yaml++
   ```
4. **Verify** the output still matches the original (semantic equality — key order and
   formatting don't matter):
   ```sh
   diff <(jq++ starter-corpus/ci-api.yml | jq -S .) \
        <(jq++ your-leaf.yaml++     | jq -S .) && echo "MATCH"
   ```
   A refactoring that changes the meaning is a failure — the generated output should
   carry the same data as the original.

## 5. Good to know

- **Keys come out sorted** and formatting is normalised — that's expected; equivalence
  is about the *data*, not the byte layout.
- **YAML comments are not preserved** through the round-trip.
- **`on:`** may appear as `'on':` in the output — that's correct (it keeps `on` a
  string rather than the YAML boolean `true`); GitHub Actions accepts it.

That's everything. Head back to the [task brief](./task-brief.md) and dive in — and
please jot down anything that confused you as you go.

[^tools]: `yq++` is a thin wrapper around `jq++`: `jq++` elaborates the input and
    emits JSON, and `yq++` converts that to YAML. (`yq++` is to `jq++` what `yq` is
    to `jq`.)

[^holder]: The stripping is done by `yq++` (a wrapper script), not by `jq++` itself —
    with plain `jq++` the key remains. You'll use `yq++`, so you don't need to mind
    this.
