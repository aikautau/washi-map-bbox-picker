# Washi Map BBox Picker

和紙ミニチュア地図の制作範囲を、地図上で選んで共有するための小さなWebツールです。

## できること

- 場所名検索と現在地表示
- `frame`（中心・サイズ・画角）または自由BBoxでの範囲指定
- 範囲を復元できる共有URLの生成
- Codexへの指示文と `osm_to_3d` 用config YAMLのコピー
- PC・スマートフォン対応

## 公共サービスへの配慮

地図にはOpenStreetMap標準タイル、検索には公開Nominatimを使用しています。検索は利用者がボタンを押したときだけ行い、同一セッション内の同一検索語はキャッシュします。大量アクセスや自動検索には使用しないでください。

- [OpenStreetMap Tile Usage Policy](https://operations.osmfoundation.org/policies/tiles/)
- [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/)

## 開発

ビルドは不要です。`index.html` をブラウザで開くか、任意の静的HTTPサーバーで配信してください。

## License

MIT
