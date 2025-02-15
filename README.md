# sotsuron-rb

比較ビルド環境の構築

```
/(root)
  /mesurement - 計測用HTML
    webpack.config.js
    /src
      ...
    /dist
    ...
  /apps - ruby.wasmアプリケーション
    /app1
    /app2
    ...
  /builders - ビルドツール
    /builder1
    /builder2
    ...
  /results - マトリックスビルド結果
    /<date>-<md5hash>
      <app_name>-<builder_name>.html
      ...
    ...
  /tmp - 一時ファイル保存
    ...
```

## 作業予定
1 = 4h

- [ ] CDNを利用した一般的なWebサイトの構成
  - [x] docker-composeでapacheを構成
  - [ ] cloudflareの設定

- [ ] 計測用HTMLの作成（ruby.wasmを除くJSやHTML） 1
  - [ ] 計測用HTMLの作成
  - [ ] JSの作成
    - [ ] HTMLで計測結果を表示する
  - [ ] サンプルruby.wasmアプリケーションの作成 1
    - [ ] 読み込み時間を計測する関数群を作成
    - [ ] rubyコードを実行する関数群を作成
    - [ ] 無変更ビルド(これをベースに派生させる) 1
    - [ ] 圧縮ビルド 1
      - [ ] 圧縮してからアクセスをするwasi-vfsのパッチ
    - [ ] minifyビルド 1
      - [ ] minify-rubyを実行するwasi-vfsのパッチ
    - [ ] コード分割ビルド 1
      - [ ] ファイルアクセスをfetch関数に置き換えたwasi-vfsのパッチ


- [ ] ビルドツールの作成
  - [ ] wasmバイナリ
    - [x] JSのグルーコードにVFS機能を仕込めるか検証する
  - [ ] ブラウザスクリプト
    - [ ] main(pkg)関数を作成
      - [ ] 引数で任意のwasmを呼び出せるようにする
      - [ ] 引数で任意のファイルをバインドできるようにする


## 各機能の責任

- 計測用ページの責任
  - 処理時間の記録/表示
  - wasm呼び出しを行う共通のAPIに準拠
  
- ruby.wasmアプリケーションの責任
  - 依存ライブラリの設定
  - Rubyコードの設定

- ビルドツールの責任
  - パッチを当てたwasi-vfsの読み込み
  - rb_wasmコマンドでwasmビルドを実行
  - ruby.wasmを出力

- マトリックスビルド機能の責任
  - ビルドツールの一括操作
  - ビルド結果の保存


## note

`bundle config set cache_all true` でbundle installのキャッシュを有効化