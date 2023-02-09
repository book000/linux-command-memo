# Node.js プロジェクトを立ち上げる手順

## 環境

- Windows 10 22H2 (Build 19045.2486)
- Node.js v18.13.0
- Yarn v1.22.19

## package.json の作成

- name
- version
- description
- repository
- author
- private

`yarn init` を使ってもよいし、そのまま `package.json` を作成して作ってもよい

```shell
❯ yarn init
yarn init v1.22.19
question name (tmp):
question version (1.0.0):
question description:
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private:
success Saved package.json
Done in 5.07s.
```

## Node.js バージョンの指定

`node -v > .node-version`, package.json で "engines": { "node": "xxx"}

```bash
# bash (Windowsの場合はWSLなど)で実行すること

# .node-version ファイルを読み取り、改行と `v` を消す
# package.json を上書きはできないので、テンポラリファイルをつくる
jq --rawfile version .node-version '.engines.node |= ($version | gsub("[v\\r\\n]"; ""))' package.json > package.json.tmp
mv package.json.tmp package.json
rm package.json.tmp
```

## TypeScript 環境の構築

TypeScript (tsconfig.json, `yarn add -D -E typescript`, `ts-node`)

## Lint ツールの導入

Lint (Prettier, ESLint, `yarn-run-all`, `lint, fix script`)

## ncc を使って 1 ファイルにコンパイル

Compile to single file (`@vercel/ncc`, `package, packing, clean script`)

## Winston でロギング

Logging with winston

https://gist.github.com/book000/b4c8394fe6a12e6ea640df0c8703eb65

https://github.com/book000/book000/issues/4

## 設定ファイル用の JSON Schema を生成

JSON Schema for Configuration file

`typescript-json-schema`

```json
{
  "scripts": {
    "generate-schema": "typescript-json-schema --required tsconfig.json Configuration -o schema/Configuration.json",
  }
}
```

```json
{
  "$schema": "../schema/Configuration.json"
}
```

## Docker で動作

https://github.com/book000/templates