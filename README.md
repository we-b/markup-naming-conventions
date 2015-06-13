# markup-naming-conventions

# we-b CSS Naming conventions
we-bでHTML/CSSをマークアップするときの命名規則です。

# ベースはBEM記法を使います。
Block、Element、Modifierの頭文字を取ったものであり、要素を3つのどれかに当てはめて命名していく方法。
- Block → ルートとなる Block 要素
- Element → Block に属する子要素
- Modifier → Block, Element に修飾を追加した要素

参考: [http://bem.info/method/definitions/](BEM-Methodology Definitionsの日本語訳)

## 命名規則

`
block
block_element
block_element-modifier
block-modifier
block-modifier_element
`

### HTML
`
<div class=“block”>
	<div class=“block_element”></div>
	<div class=“block_element-modifier”></div>
</div>
<div class=“block-modifier”>
	<div class=“block-modifier_element”></div>
</div>
`

### SCSS
`
$techcamp-color: #dc5041;
$techcamp-color-green: #43ac6a;

.block {
	border: 1px solid #000;
}

.block-modifier {
	@extend .block;	
	color: $techcamp-color-green;
}

.block_element {
	background-color: #eee;
}
	
.block_element-modifier {
	@extend .block;
	color: $techcamp-color;
}

.block-modifier_element {
	@extend .block_element-modifier;
}
`

# we-b では Bootstrap を使います。
[Bootstrap · The world's most popular mobile-first and responsive front-end framework.](http://getbootstrap.com/)

だいたいのコーポネーントはあるので、極力 Bootstrap を使いましょう.
- Boostrasp 以外の HTML / CSS を書くときは新しくファイルを作って style.css.csss を作りましょう。


# その他のCSSの書き方
## セレクタの後には、改行を入れましょう
改行があると無いとで見やすがダンチです。
- Example
`
.example {
	color: #000;

	.example_title {
		font-size: 36px;
	}
}

.example-body {
	background-color: #eee;
}
`

## 変数を使いましょう
SCSS では、変数が使えるので色やフォントなど固定できるものは使いましょう。
`
$baseColor: #dc5041; //tech-camp red color #dc5041
$fz-regular: 14px; // font-size: 14px;

h1 {
  background-color: $baseColor;
  font-size: $dz-regular;
  color: #fff;
}
`

## 色を薄く・濃くする場合は色は新しく作らない
SCSS では、色を薄く・濃くすることができます。新たに１６進数を指定するのではなく、こちらで色を変更しましょう。
`
h1 {
	background-color: lighten($baseColor, 10%); // #dc5041 を　10％　薄くする
	color: darken(#fff, 20%); // #fff を 20% 濃くする
	
}
`

##  上書きは極力避ける
CSS で上書きを繰り返すと、予期せぬところでCSS が適用できない場面が出てきます。
上書きをせずに、Modifier を作り、スタイルを変えていきましょう。
`
// ダメな例

.btn {
	background-color: $baseColor;
	border: 1px solid darken($baseColor, 10%);
	padding: 10px;
	border-radius: 3px;
	display: inline-block;
}

// いい例
.btn {
	border-radius: 3px;
	display: inline-block;
}

.btn-primary {
	@extend .btn;
	background-color: #fff;
	border: 1px solid $baseColor;
}

.btn-large {
	@extend .btn;
	padding: 20px;
}

.btn-primary-large {
	@extend .btn-primary;
	@extend .btn-large;
}

 `
 

