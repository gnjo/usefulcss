# development-complex
開発に関する要点
```js
```
共通関数。
```
共通関数は大きく二つ。
fn.xxx:頻度の高い操作
is.xxx:判定も関数化する。
```
全体オブジェクト。
```
外部に一つが望ましい。
let app={}
```
全体オブジェクトへの追加。
```
一つの全体オブジェクトに対して追加を行う。
機能単位でクロージャーで囲う。
初期化が必要な場合はもう一つ関数が増える。
HTMLを使う表示部分と計算部分は別の関数とし、表示部から計算関数を呼ぶ。
;(function(app){

 app.xyzcalc=()=>{ ...Dont DOM }
 app.xyz=()=>{ ... }
 app.xyzInit=()=>{ ... }
})(app);
```
開始関数
```
開始関数は一つのみ。asyncを付けるとネストの深さを緩和できる。
app.init=async ()=>{
 await xxxx
 await xxxx
}
app.init();////////////////
```
エラー表示
```
throw new TypeErrorかreturn console.logを使う。
前者推奨
 throw new TypeError('xyz');
 return console.log('xyz');
```
要素
```
要素は必ずラッパーを被せる。特にimgのようなafter要素を使用出来ない要素は必ずである。
.wrap
 .ed
.wrap
 img
```
要素の追加
```
htmlを文字列で出力し、そのhtmlに対してフラグメントを作成し、追加する。
生成した要素に変更を加えたいだろうが、極力文字列で解決する。
メタプログラミングの方がユーザ操作をブロッキングしないからである。
要素のオブザーバ関数がある為、積極的にdata-xxx情報を追加し、トリガーとする。
内部データの変更をトリガーとするなら、Proxyも考慮する。
let html='<div class="wrap"><div data-xyz="abc"></div></div>'
let fr=fn.fr(html)
fn.a2(fr,document.body)
```
要素全体の追加
```
初回起動時には、全体のhtmlを生成しフラグメントへ書き込み、一度だけ描写した方が高速である。
生成した要素を極力htmlで出力する理由でもある。
この場合、要素一つの追加、要素全体の追加を考える必要がある。
ほぼ同じ機能になるが、描画を一度だけにする事は重要である。
app.draw();
app.draw(allflg)
```
背景色と文字色
```
背景色と文字色はコントラスト比で基準を設ける。
16> rate 明る過ぎる。
16 rate 明瞭
7.0 rate 明瞭
4.5 rate 判別できる。
2.0 rate 暗く見える。
2.0 < rate 見えない。 
```
速度計測
```
let t0,t1,time
t0=performance.now()
....
t1=performance.now()
time=t1-t0;
console.log(time,"[ms]")
```


