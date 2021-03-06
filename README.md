# TextAlive App APIを利用したWebアプリケーション

<img src="https://github.com/tacrice/to-the-future/blob/main/screenshots/screenshot1.png" width="600">


本アプリケーションは初音ミク「マジカルミライ 2020」プログラミング・コンテスト応募作品です  
https://magicalmirai.com/2020/procon/

本アプリケーションはTextAlive App APIを利用しています  
https://developer.textalive.jp/packages/textalive-app-api/

本アプリケーションはThree.jsを利用しています  
https://threejs.org/

# 楽曲の再生
ページ読み込み後、画面全体(下部の一部を除く)をクリック・タップすることで再生・一時停止を行います  
また、下部のプログレスバーを操作することによって楽曲をシークすることもできます

# 違う楽曲で試すには
本アプリケーションは「愛されなくても君がいる by ピノキオピー feat. 初音ミク」での演出を推奨していますが、URLのクエリパラメータで下記を指定すると異なる楽曲で演出を試せます
- グリーンライツ・セレナーデ by Omoi feat. 初音ミク  
 クエリパラメータ: `s=1`
- ブレス・ユア・ブレス by 和田たけあき feat. 初音ミク  
 クエリパラメータ: `s=2`

# アピールポイント
## 歌詞が見えにくくならないような工夫
### 文字の重なり
そのまま描画してしまうと文字が重なり、読みにくくなってしまうので背景色と同じ色の少し大きめの文字を通常文字の前に擬似輪郭線として描画することで重なっても見やすくしてます。
### タイミングの重なり
また、タイミングがほぼ同じケースに対応するため、文字ごとの表示タイミングを使うのではなく、単語(word)を文字数で均等に分散することで重なりを軽減してます
### 長音符
長音符("ー")は角度がついていると見た目がよくなかったので、文字ごと回転させる処理を入れました

<img src="https://github.com/tacrice/to-the-future/blob/main/screenshots/screenshot4.png" width="400">

## キューブについて
マジカルミライといえばキューブのイメージだったので作成しました
### メッシュ
threejsのboxジオメトリをそのまま使うと、マテリアルIndexの割り当てが各6面になっているので、6面x2triangleの12triangleのマテリアルIndexをランダムに割り振ることで表現しました  
またこのマテリアルのカラーはピアプロキャラクターをイメージしたカラーを使用しています
### 生成タイミング
TextAlive App APIの歌声の声量(vocalAmplitude)を積み重ねて一定数を超えたときに生成しています  
なので盛り上がっている場面ではより多く生成され、しっとりとしている場面では生成数が抑えられます  
またキューブのサイズもその時点での歌声の声量をベースに大きくしたり小さくしたりしています

## サビの演出
ガラッと印象を変えるように場面転換を行いました

### 場面転換
驚きを与えるために、サビに入る遷移はビートを使用したサークルの円の内側からパキッと変化するようにしました  
逆にサビから戻るところはシームレスに演出してます

<img src="https://github.com/tacrice/to-the-future/blob/main/screenshots/screenshot2.png" width="400">
<img src="https://github.com/tacrice/to-the-future/blob/main/screenshots/screenshot3.png" width="400">

### ラストサビ演出
こちらはさらなる驚きと盛り上がりを与えるために、星屑の演出も追加しました
星屑は大きなポイントマテリアルのジオメトリを1セット2つずつ用意し、ベルトコンベアのように動作することで無限に流れていくようにしてます
またこちらにもピアプロキャラクターをイメージしたカラーを少量配置しています

<img src="https://github.com/tacrice/to-the-future/blob/main/screenshots/screenshot5.png" width="600">

## スマートフォンでの視聴
PCだけではなくスマートフォン(iPhone)での視聴も確認してます
また、できるだけリサイズにも対応しているので縦横どちらでも見えるようになっています
