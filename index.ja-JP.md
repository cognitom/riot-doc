

title: Riot 2.2 | A React-like UI library
subtitle: なぜ Riot?
description: そして、なぜ新たなUIライブラリが必要なのか
body_id: riot-home
hero: true

====

# 1. カスタムタグ

RiotはIE8以降の全てのブラウザで、カスタムタグを実現します。

``` html
<todo>

  <!-- layout -->
  <h3>{ opts.title }</h3>

  <ul>
    <li each={ item, i in items }>{ item }</li>
  </ul>

  <form onsubmit={ add }>
    <input>
    <button>Add #{ items.length + 1 }</button>
  </form>

  <!-- logic -->
  <script>
    this.items = []

    add(e) {
      var input = e.target[0]
      this.items.push(input.value)
      input.value = ''
    }
  </script>

<todo>
```
カスタムタグは、関連するHTMLとJavaScriptをくっつけて再利用可能なコンポーネントとしてまとめます。React + Polymerに、"楽しい"文法と小さな学習曲線が一緒になったものをイメージしてください。


### ヒューマンリーダブル

カスタムタグはHTMLで複雑なビューの構築を可能にします。あなたのアプリケーションはこんな感じになるでしょう:

``` html
<body>

  <h1>Acme community</h1>

  <forum-header/>

  <forum-content>
    <forum-threads/>
    <forum-sidebar/>
  </forum-content>

  <forum-footer/>

  <script>riot.mount('*', { api: forum_api })</script>
</body>
```

HTMLの文法はWebの *デファクト* 言語であり、ユーザインターフェースを構築するためにデザインされています。文法はシンプルで明確、入れ子構造が備わっていて、属性はカスタムタグにオプションを提供するための簡潔な方法です。

<span class="tag">メモ</span> タグファイルは、ブラウザで実行する前に、JavaScriptに [変換されます](compiler.html)。


### 仮想DOM
- 最小のDOMの更新とリフロー
- データは一方通行: 更新とアンマウントは親から子へ伝播します。
- テンプレートは高いパフォーマンスを得るため、プリコンパイルされキャッシュされます。
- 細かい制御のためのライフサイクルイベント
- アイソモーフィックアプリケーションを実現する、カスタムタグのサーバサイドレンダリング


### 標準に近い
- 独自形式のイベントシステムはなし
- IE8でも使える標準化されたイベント
- レンダリングされたDOMは、自由に他のツールから操作可能
- 余計なHTMLのルート要素や`data-`属性を使う必要なし
- jQueryとの親和性が高い


### お気に入りのツールと一緒に
- タグファイルは、CoffeeScriptやJade、Typescript、LiveScript、ES6や、その他の好きな[any pre-processor](compiler.html#pre-processors)でOK。
- NPMやCommonJS、AMD、Bower、Componentが使えます。
- [Gulp](https://github.com/e-jigsaw/gulp-riot)や[Grunt](https://github.com/ariesjia/grunt-riot)、[Browserify](https://github.com/jhthorsen/riotify)のプラグインでコンパイル



# 2. シンプルでミニマリスト

ミニマリズムが、Riotを他のライブラリと一線を画すものにしています。


### 1. 楽しい文法

デザインのゴールの一つは、できる限り最小の"boilerplate"で使える、協力な文法を導入することです。

- 強力なショートカット: `class={ enabled: is_enabled, hidden: hasErrors() }`
- 余計なことを考えなくてOK。`render`とか`state`、`constructor`、`shouldComponentUpdate`などなど。
- インターポレーション: `Add #{ items.length + 1 }` あるいは `class="item { selected: flag }"`
- ロジック部分を`<script>`タグで囲むのはオプション
- コンパクトなES6のメソッドの書き方


### 2. 小さな学習曲線

Riotは他のURライブラリと比較して、10か100倍APIが少ないです。

1. 覚えることが少ない。見なきゃいけない本もチュートリアルも少ない。
2. 独自形式なものが少なく、標準的なものが多い


### 3. サイズが小さい

<small><em>react.min.js</em> – 127KB</small>
<span class="bar red"></span>

<small><em>polymer.min.js</em> – 120KB</small>
<span class="bar red" style="width: 94%"></span>

<small><em>riot.min.js</em> – 6.7KB</small>
<span class="bar blue" style="width: 4.8%"></span>


1. 少ないバグ
4. パースが早く、ダウンロードも容易
3. エンベッダブル(組込可能): ライブラリはアプリケーション本体より小さくあるべき
4. メンテナンスの手間が少ない: Riotのメンテナンスのために大きなチームを必要としない

### 4. 小さくて、必要十分

Riotはモダンなクライアントサイドのアプリケーションを作るための、基本的な構成単位をすべて備えています。

- ユーザインターフェースを構築するための"Reactive"なビュー
- 分離されたモジュールのAPIを作るためのイベントライブラリ
- URLと「戻る」ボタンを処理するルータ

Riotは「オープンスタック」です。つまり、フレームワーク特有のイディオムを避けたい開発者向けです。一般的であることで、好きなデザインパターンを適用したり、混ぜたりすることができます。Facebook Fluxのようなシステムを[つくるこ](https://github.com/jimsparkman/RiotControl).


==== .tweets.section

Today I have used #riotjs 2.0 for the first time and I could admit that It will be a long term relationship #js highly recommended. [@gianlucaguarini](https://twitter.com/gianlucaguarini/status/559756081862574080)

I liked the idea of #reactjs with #flux but I like #riotjs with #riotcontrol even better!
[@tscok](https://twitter.com/tscok/status/580509124598829056)

I’m loving riot.js! So much power packed into 3.5kb. [@ncthis](https://twitter.com/ncthis/status/575204037877833728)

looking at RiotJS https://muut.com/riotjs/  - blown away by its simplicity. [@defeated](https://twitter.com/defeated/status/559215403541757952)

Played with riot.js and like it so much more than react. Minimalistic, fast and a comprehensible API. [@juriansluiman](https://twitter.com/juriansluiman/status/560399379035865088)

I looked at the riot.js example, and it feels so clean, it's scary. [@paulbjensen](https://twitter.com/paulbjensen/status/558378720403419137)

==== .section.narrow

# まとめ

Riotはサイズは小さいままに、React + Polymer + モデル + ルーティング を実現するライブラリです。今日から使えます。IE8でも。とにかくシンプルで、すごく軽い。車輪の再発明をするのではなく、これらのツールの良いとこ取りで、可能な限りシンプルにしました。

私たちは、テンプレートではなく、再利用可能なコンポーネントにフォーカスするべきです。Reactの開発者曰く:

> 「テンプレートは、問題ではなく、技術を分けるだけだ」

同じコンポーネントの中で、レイアウトとロジックを一緒に持てば、全体のシステムはより簡潔になります。この重要な洞察について、Reactに敬意を示したいと思います。


#### Muut blog: [From React to Riot 2.0](/blog/technology/riot-2.0/) | .tall
