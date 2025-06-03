```dart
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _janken = <String>['グー', 'チョキ', 'パー'];

  @override
  Widget build(BuildContext context) {                       
    return Scaffold(
      appBar: AppBar(　　　　　　　　　　　　　　　　　　　　
        title: Text('App Name'),　　　　　　　　　　　　　　
      ),　　　　　　　　　　　　　　　　　　　　　　　　　　
      body: Center(　　　　　　　　　　　　　　　　　　　　
        child: Column(                                  
          mainAxisAlignment: MainAxisAlignment.start,　　
          mainAxisSize: MainAxisSize.max,　　　　　　　　　
          crossAxisAlignment: CrossAxisAlignment.stretch,　
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),             
              child: Text(                               
                _message,　　　　　　　　　　　　　　　　　
                style: TextStyle(　　　　　　　　　　　　　
                  fontSize: 32.0,　　　　　　　　　　　　　
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),　　　　　　　　　　　　　　　　　　　　　　
            TextButton(　　　　　　　　　　　　　　　　　　
              onPressed: buttonPressed,　　　　　　　　　、
              child: Padding(　　　　　　　　　　　　　　　
                padding: EdgeInsets.all(10.0),　　　　　
                  "Push me!",　　　　　　　　　　　　　　　
                  style: TextStyle(　　　　　　　　　　　
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto"),
              ~ 略 ~
    void buttonPressed() {
    setState(() {
      _message = (_janken..shuffle()).first;
     
     これは、「ぐー」「ちょき」「ぱー」からランダムに手を選んで表示する サンプル。「Push me!」をクリックすると、ランダムにじゃんけんの手を表示する。またここでは_messageに、_janken..shuffle()で返している。またカスケード記法を使い元のオブジェクトからfirstで最初の要素を取り出している。

      ~TextButtonについて~
      　UIの外観などを持たない平面のボタン「TextButton」というクラスで用意される。またFlutter Stdioでは「FlatButton」 というアイコンがTextButtonに相当する。
      extButton自体、ただ表示するだけでなくクリックすると何らかの処理を実行したりするために利用される

      ~テキストの表示~
       TextButtonにテキストを表示するには、内部にTextを組み込む必要がある。つまりウィジェットをテキストの代わりに組み込むことで表示を変えることができる。

PaddingはTextを組み込む際に,まずPaddingというウィジェットが組み込まれ、その中にchildTextが組
込まれている。padding自体は名前の通りパディング（余白）を表示するためのコンテナのこと。この中に
ウィジェットを組み込むと、ウィジェットの周囲に余白を作成する。余白は、paddingプロパティにEdgeInsets
を使って設定する。

　~様々なボタン~
ElevatedButton...TextButtonと似たような働きをした少し立体的に表示するボタン。
IconButton ...クリックして利用するボタン。プレビューにドラック&ドロップするとカラーぱれっどと
　　　　　　　　アイコンの種類、「Size」をプロパティに表示され指定できる。
FloatingActionButton...アイコンを表示するボタンに使われている。ScaffoldのfloatingActionButtonに
　　　　　　　　　　　　　インスタンスを設定することで画面の右下に自動的にボタンが追加表示される
　　　　　　　　　　　　　ようになる。
RawMaterialButton... 表示の色などテーマなどによる初期値の設定の影響を受けないボタンです。そのため
　　　　　　　　　　　　自身で使用する色はすべて設定して利用する。
