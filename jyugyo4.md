class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _janken = <String>['グー', 'チョキ', 'パー'];

  @override
  Widget build(BuildContext context) {                       
    return Scaffold(
      appBar: AppBar(　　　　　　　　　　　　　　　　　　　　~TextButtonについて~
        title: Text('App Name'),　　　　　　　　　　　　　　UIの外観などを持たない平面のボタン
      ),　　　　　　　　　　　　　　　　　　　　　　　　　　「TextButton」というクラスで用意され
      body: Center(　　　　　　　　　　　　　　　　　　　　る。またFlutter Stdioでは「FlatButton」
        child: Column(                                  というアイコンがTextButtonに相当する。
          mainAxisAlignment: MainAxisAlignment.start,　　TextButton自体、ただ表示するだけでなく
          mainAxisSize: MainAxisSize.max,　　　　　　　　　クリックすると何らかの処理を実行したり
          crossAxisAlignment: CrossAxisAlignment.stretch,　するために利用する。
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),             ~アイコンの表示~
              child: Text(                               TextButtonにテキストを表示するには、
                _message,　　　　　　　　　　　　　　　　　内部にTextを組み込む必要がある。つまり
                style: TextStyle(　　　　　　　　　　　　　ウィジェットをテキストの代わりに組み込
                  fontSize: 32.0,　　　　　　　　　　　　　むことで表示を変えることができる。
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),　　　　　　　　　　　　　　　　　　　　　　...このプログラムでは「ぐー」「ちょき」「
            TextButton(　　　　　　　　　　　　　　　　　　ぱー」からランダムに手を選んで表示する
              onPressed: buttonPressed,　　　　　　　　　サンプル。「Push me!」をクリックすると、
              child: Padding(　　　　　　　　　　　　　　　ランダムにじゃんけんの手を表示する。
                padding: EdgeInsets.all(10.0),　　　　　またここでは_messageに、_janken..shuffle
                child: Text(                           ()で返している。またカスケード記法を使い
                  "Push me!",　　　　　　　　　　　　　　　元のオブジェクトからfirstで最初の要素を
                  style: TextStyle(　　　　　　　　　　　取り出している。
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto"),
              ~ 略 ~
    void buttonPressed() {
    setState(() {
      _message = (_janken..shuffle()).first;

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
