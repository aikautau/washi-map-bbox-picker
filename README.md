# Washi Map BBox Picker

和紙ミニチュア地図の制作範囲を、地図上で選んで共有するための小さなWebツールです。

## できること

- 場所名検索と現在地表示
- `frame`（中心・サイズ・画角）または自由BBoxでの範囲指定
- デスクトップ（3840×2160）、スマホ（1440×3120）、たて（1920×2400）の画角
- A4・A3（たて/よこ）の白黒ワイヤー印刷用サイズと、`wire_print_config.py` のコマンド生成
- 範囲を復元できる共有URLの生成
- Codexへの指示文と `osm_to_3d` 用config YAMLのコピー
- 浅瀬・雪化粧・夕凪・桜の選択と、フルconfig YAMLの保存
- PC・スマートフォン対応

## YAMLから自分で制作する

「中心＋サイズ」で場所・サイズ・画角を選び、地域名（保存名）と表現を指定します。
フルconfigは初期状態で有効です。「YAMLを保存」で取得したファイルを
`osm_to_3d/configs/`に置き、リポジトリ直下で実行します。

```bash
/opt/homebrew/Caskroom/miniconda/base/envs/geo/bin/python build_map.py --config configs/new_area.yaml
```

ファイル名は指定した地域名に合わせてください。YAMLには`name`、`bbox`、PLATEAU建物指定、
選択した`style.preset`、`render`の解像度・256サンプル・GPU指定が入ります。
中心＋サイズを使っても、フルconfigは確定したBBoxと解像度で書き出します。
フルconfigを外すと、以前と同じ`frame`または`bbox`の範囲部分だけをコピーできます。

自由BBoxは選んだ範囲の縦横比を保ち、高さ2400pxから幅を計算します。
デスクトップ・スマホ・たての固定サイズで作る場合は「中心＋サイズ」を使ってください。
A4・A3ではこれまでどおりワイヤー印刷用の生成コマンドを出します。

表現をYAMLで指定する場合の完成画像は`out/<地域名>/render_credit.png`です。
同じ地域の色違いを別ファイルへ出す場合は、既存configを使い、例えば
`--preset yukigesho`を付けます。取得記録・キャッシュは保持し、完成画像は目視で検品します。

## 公共サービスへの配慮

地図にはOpenStreetMap標準タイル、検索には公開Nominatimを使用しています。検索は利用者がボタンを押したときだけ行い、ブラウザごとに最低1.1秒の間隔を空けます。同じ検索語の結果はブラウザ内へ7日間・最大50件保存し、再問い合わせを避けます。大量アクセスや自動検索には使用しないでください。

検索履歴のキャッシュはブラウザのサイトデータを消去すると削除できます。

- [OpenStreetMap Tile Usage Policy](https://operations.osmfoundation.org/policies/tiles/)
- [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/)

## 開発

ビルドは不要です。`index.html` をブラウザで開くか、任意の静的HTTPサーバーで配信してください。

外部リソースはCSPでLeaflet CDN、OpenStreetMapタイル、Nominatimだけに制限しています。インラインスクリプトを変更した場合は、CSP内のSHA-256ハッシュも更新してください。

紙サイズ（A4・A3）のbbox計算は `osm_to_3d` の `tools/wire_print_config.py` と同じ定数・同じ式です。片方を変えたらもう片方も合わせてください。configそのものは生成器だけが書きます。

## License

MIT
