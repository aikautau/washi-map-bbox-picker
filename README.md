# Washi Map BBox Picker

和紙ミニチュア地図の制作範囲を、地図上で選んで共有するための小さなWebツールです。

## できること

- 場所名検索と現在地表示
- `frame`（中心・サイズ・画角）または自由BBoxでの範囲指定
- 範囲を復元できる共有URLの生成
- Codexへの指示文と `osm_to_3d` 用config YAMLのコピー
- PC・スマートフォン対応

## 公共サービスへの配慮

地図にはOpenStreetMap標準タイル、検索には公開Nominatimを使用しています。検索は利用者がボタンを押したときだけ行い、ブラウザごとに最低1.1秒の間隔を空けます。同じ検索語の結果はブラウザ内へ7日間・最大50件保存し、再問い合わせを避けます。大量アクセスや自動検索には使用しないでください。

検索履歴のキャッシュはブラウザのサイトデータを消去すると削除できます。

- [OpenStreetMap Tile Usage Policy](https://operations.osmfoundation.org/policies/tiles/)
- [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/)

## 開発

ビルドは不要です。`index.html` をブラウザで開くか、任意の静的HTTPサーバーで配信してください。

外部リソースはCSPでLeaflet CDN、OpenStreetMapタイル、Nominatimだけに制限しています。インラインスクリプトを変更した場合は、CSP内のSHA-256ハッシュも更新してください。

## License

MIT
