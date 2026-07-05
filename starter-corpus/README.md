# Fresh Eyes — Starter Corpus

These are four small GitHub Actions CI workflows for a repository that builds and
pushes a container image for each of four services (`api`, `web`, `worker`,
`scheduler`). They share a lot of structure.

Your task (see [`../task-brief.md`](../task-brief.md)): refactor them with
JSON++ / jq++ so the shared structure is expressed once and each file keeps only
what makes it different — then verify the generated output matches these originals.

---

# Fresh Eyes — スターターコーパス

これは、4 つのサービス（`api`、`web`、`worker`、`scheduler`）それぞれのコンテナ
イメージをビルドしてプッシュするリポジトリの、小さな GitHub Actions CI ワークフロー
4 つです。多くの構造を共有しています。

課題（[`../task-brief.ja.md`](../task-brief.ja.md) を参照）: JSON++ / jq++ を用いて
共通する構造を一度だけ記述し、各ファイルには差分だけを残すようにリファクタリングし、
生成された出力がこれらの元ファイルと一致することを確認してください。
