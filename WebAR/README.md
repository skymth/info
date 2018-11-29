
## webARとは...

AR技術をWebブラウザ上から利用できるようにしたもの。今回はfirefoxなどを開発しているmozillaが出している [AFrame](https://aframe.io/docs/0.8.0/introduction/)と、[AR.js](https://github.com/jeromeetienne/AR.js)を駆使してARを作成していきます！


## AFrame
AFrameは言った通り、mozilaが開発しているjsのライブラリです。
WebVRフレームワークで、以下のような特徴を持っています。

- WebGLの知識がなくても、簡単にVR環境を構築可能
- レスポンシブなVRサイトを作れる
- MITライセンスでソースが公開

## AR.js

- インストールの必要性がない
- 軽量かつ高速
- WebGLとWebRTCで動作可能
- mobileだと今の所, safariのみ？

## 今回やること

AR空間上に、自分が表示したい文字を表示する。
デバイスのカメラの起動、映像を認識したマーカーとオブジェクトの紐づけをAR.jsで行い、表示するオブジェクトの作成をAFrameでする感じです。

- A-Frameライブラリの読み込み

```html:
<script src="https://aframe.io/releases/0.8.0/aframe.min.js"></script>

```

- AR.jsライブラリの読み込み

```html:
<script src="https://jeromeetienne.github.io/AR.js/aframe/build/aframe-ar.js"></script>
```

のような感じで、ライブラリを使用します。

## 実装

`index.html`を用意して以下のようにcordingしていきます。

```html:index.html
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width,intial-scale=1">
        <title>WebAR</title>
    </head>
    <body style="margin:0px; overflow:hidden;">
        <script src="https://aframe.io/releases/0.8.0/aframe.min.js"></script>
        <script src="https://jeromeetienne.github.io/AR.js/aframe/build/aframe-ar.js"></script>

        <a-scene embedded arjs="debugUIEnabled:false; sourceType: webcam;">
            <a-marker preset="custom" type='pattern' url="my-icon-marker.patt">
              <a-text value="My name is soeyu!\n Nice to meet you!" position=" 0 0 1" align="center" rotation="-90 0 0" color="#7993ff">
              </a-text>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

### 説明


```html:
<a-scene embedded arjs="debugUIEnabled:false; sourceType: webcam;"> // ※1
		<a-marker preset="custom" type='pattern' url="my-icon-marker.patt"> // ※2
			<a-text value="My name is soeyu!\n Nice to meet you!" position=" 0 0 1" align="center" rotation="-90 0 0" color="#7993ff"> // ※3
			</a-text>
		</a-marker>
	<a-entity camera></a-entity>
</a-scene>
```

1. A-Frameの”a-scene”タグにAR.jsを紐づける
1. markerの設定、presetタグ内でmarkerの設定ができる。<br> ([AR.ja marker generater](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html): 自分の好きなmarkerの作成が可能)
1. markerを認識した際に、valueタグ内の文字列を表示する。

<br>

と言うようにコード量もあまり多くなく、ARができます。

## demo

上の実装であったコードを実際にスマートフォンで確認するため、無料ホスティングサービスである、[Netlify Drop](https://app.netlify.com/) を利用して確認します。githubのアカウントを持っていればすぐに利用できます。

<img width="1128" alt="Screen Shot 2018-11-29 at 19.07.53.png" src="https://qiita-image-store.s3.amazonaws.com/0/192279/b02a659d-ffd8-52d4-68ce-d8663b1274ad.png">

`index.html`を含むディレクトリをドラッグ&ドロップすれば、URLが発行されるのでそこにアクセスすれば確認できます！



### demo movie
![ezgif.com-video-to-gif.gif](https://qiita-image-store.s3.amazonaws.com/0/192279/37dd11c3-6614-67ba-2f77-68f353d31728.gif)

## 最後に

[poly](https://poly.google.com/) などで上げられている、オブジェクトを使用すれば、以下の画像のようにダウンロードしたオブジェクトを表示することができます。<br>

<img src="https://qiita-image-store.s3.amazonaws.com/0/192279/20e97255-21f3-ed88-65eb-77668e509527.jpeg" width="200px">>

webARなら誰もがとっつきやすく、簡単に実装できるのでもし興味があったら皆さんもぜひやってみてください。

## reference

- [AR.js](https://github.com/jeromeetienne/AR.js/blob/master/README.md)
- [A-Frame](https://aframe.io/)
- [poly](https://poly.google.com/)
- [netlify](https://app.netlify.com/)
- [Three.js](https://jeromeetienne.github.io/AR.js-docs/docs/)
