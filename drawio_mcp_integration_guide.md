# Draw.io MCP 統合手順書

Draw.io MCPをシステムに統合し、AIによる自動図面生成を有効にするための手順です。

## 1. 構成の更新
`~/.gemini/antigravity/mcp_config.json` に以下のエントリを追加しました：

```json
"drawio": {
  "command": "npx",
  "args": ["-y", "drawio-mcp"]
}
```

## 2. ツールとしての活用
組み込みが完了すると、AIエージェントは以下の操作が可能になります：
- **Mermaidからの図面生成**: Mermaid.jsのコードをDraw.ioのXML形式に変換し、ブラウザで開く。
- **XML編集**: 既存のDraw.io XML（mxGraph）の読み書き。
- **アーキテクチャの可視化**: Rust/PostgreSQLなどのシステムの構成図を自動描画。

## 3. 実行例
エージェントに対して「このアーキテクチャをDraw.ioで図解して」と指示することで、即座にブラウザ上で編集可能な図面が展開されます。
