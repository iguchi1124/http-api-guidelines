# HTTP API作業の共通ルール

HTTP APIの設計・実装・レビュー、OpenAPI仕様の編集時には、[HTTP API開発ガイドライン](skills/http-api-guidelines/references/http-api-guidelines.md)を読んで適用する。

- 規約本文の唯一の編集元は上記ファイルとする。
- 配布単位はskills/http-api-guidelines/のAgent Skills形式とする。ホスト固有の読込手順はREADME.mdで案内する。
- 未決定事項や例を、新たな必須ルールとして扱わない。
- コミットメッセージはConventional Commits 1.0.0に従う。新機能はfeat、不具合修正はfix、破壊的変更は!またはBREAKING CHANGE:で示す。
- 共有ルールを変更するときはAGENTS.mdとCLAUDE.mdの同等の指示を整合させ、ツール固有の指示は保持する。
