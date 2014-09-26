#BeaconWorkshopユーザー定義データ・カスタマイズマニュアル

このドキュメントでは「ビーコンワークショップアプリ」(以下、BeaconWorkshop)で取り込むことができるユーザー定義データをカスタマイズする方法について説明します。  
アプリの使い方は [BeaconWorkshopマニュアル](manual.md)をご参照ください。


###用意するもの
- テキストエディタ  
htmlファイルやcssファイルを編集する際に必要です
- 画像編集ソフト  
自作画像を作ったり加工したりする場合に必要です

###メインマップ画面の背景を変更する
index.html内で指定している画像ファイル名を変更する。もしくは、background.pngを上書き更新する。

例:  
変更前 ```<img src="images/background.png" />```  
変更後 ```<img src="images/bg.png" />```

###メインマップ画面上のビーコンの位置を変更する
index.html内の以下のようなビーコンアイコンの位置はスタイルシートで指定します。

```html
<a href="1-101.html" id="1-101" class="beacon region-1-101"></a>
```

この例では、ビーコンアイコンのリンク(aタグ)とスタイルシート(style.css)は、region-1-101 というクラス名で紐づいています。

```html
.region-1-101 {
	position: absolute;
	left: 110px;
	top: 400px;
}
```

このクラスのleftおよびtopプロパティを変更することでビーコンアイコンの表示位置を変更することができます。


###メインマップ画面上のビーコンの画像を変更する
index.html内の以下のようなビーコンアイコンの画像はスタイルシートで指定します。

```html
<a href="1-101.html" id="1-101" class="beacon region-1-101"></a>
```

スタイルシート(style.css)では、ビーコンアイコンのリンク(aタグ)で適用されている beacon というクラス名でデフォルトのビーコン画像(images/beacon-off.png)が指定されています。この画像を更新するか、追加した画像を指定します。ビーコン領域外の状態をあらわすout-of-regionクラスも同様に変更してください。

```
.beacon {
	background-image: url(images/beacon-off.png);
	width: 32px;
	height: 32px;
	display:block;
}

.out-of-region  {
	background-image: url(images/beacon-off.png);
}
```


###ビーコン領域内にいる場合のビーコン画像を変更する
スタイルシート(style.css)のwithin-regionクラスの画像ファイル名指定を変更します。

```
.within-region  {
	background-image: url(images/beacon-on.png);
  -webkit-animation: anim 1s infinite;
}
```

###訪問済みビーコン画像を変更する
スタイルシート(style.css)のvisitedクラスの画像ファイル名指定を変更します。

```
.visited
{
	background-image: url(images/beacon-on.png);
}
```


###メインマップ画面上のビーコンの数を増やす(減らす)
index.html内のビーコンリンクをコピー(削除)します。追加する場合、リンク先アドレスとidは適宜変更してください。

```
  <a href="1-101.html" id="1-101" class="beacon region-1-101"></a>
  <a href="hoge.html" id="12345" class="beacon region-12345"></a>
```

###メインマップ画面上のビーコンタップ時に表示する個別コンテンツ画面を変更する
index.html内のビーコンリンクをのリンク先アドレスを変更します。以下に例を示します。

変更前

```
  <a href="1-101.html" id="1-101" class="beacon region-1-101"></a>
```

変更後

```
  <a href="hoge.html" id="1-101" class="beacon region-1-101"></a>
```

###ビーコンに反応した際に表示するコンテンツを変更する
major:1, minor:101のビーコンに反応した際に表示する個別コンテンツを変更する手順を説明します。

はじめにビーコン領域定義ファイル(regions.plist)からビーコン情報に合致する要素(dict)を探し、identifierを特定します。以下の例では 1-101 という値が identifier になります。

```
	<dict>
		<key>identifier</key>
		<string>1-101</string>
		<key>major</key>
		<integer>1</integer>
		<key>minor</key>
		<integer>101</integer>
	</dict>
```

次に、表示コンテンツ定義ファイル(contents.plist)から、先ほどの 1-101 という値を Region identifier キーの値に持つ要素を探します。  
この例では、以下の要素が見つかりました。

```
	<dict>
		<key>Region identifier</key>
		<string>1-101</string>
		<key>Title</key>
		<string>南出入口</string>
		<key>Content URL</key>
		<string>1-101.html</string>
	</dict>
```

見つかったdict要素内のContent URLキーを変更します。  
以下の例では 1-101.html を fuga.html に変更しました。

```
	<dict>
		<key>Region identifier</key>
		<string>1-101</string>
		<key>Title</key>
		<string>南出入口</string>
		<key>Content URL</key>
		<string>fuga.html</string>
	</dict>
```


###コンプリート画面の内容を変更する
completed.html を適宜編集してください。

###コンプリート画面を表示しないようにする
completed.htmlを削除してください。