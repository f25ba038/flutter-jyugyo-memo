# 入力のためのUI 

| UI名 | 役割 |
|:---|:---:|
|TextField... |テキストを入力するUIウィジェット |
| Chackbox...|ON,OFFといった二者択一と値を入力する |
|Switch...|スイッチのON,OFFするウィジェット※ChackBoxと役割はほぼ同じ|
|Radio...|複数項目から一つを選ぶUIウィジェット※◎のようなもの|
|DrpdownButton...|複数の項目から一つを選ぶウィジェット※▼~文字~のような感じ|
|PopupMenuButton...|ポップアップメニューを呼び出すためボタン※Dropdownbottonと似たような役割で「⋮」を利用する|
|Slider...|数値をアナログ的に入力するドラッグして動かすノブで左右に動かし値を設定する|

#  アラートとダイアログ
## show関数について
　アラート(必要に応じて画面にUI画面が表示されるもの)などを画面に表示するための関数。「showDialog」という関数で利用する。
```dart
showDialog(
    context:《BuildContext》,
    builder:《WidgetBuilder》
)
```
contextにはBuildContextインスタンス指定をする。そして、BuildContextというクラスはウィジェットのベースとなる。
builderはWidgetBuilderというクラスでtypedef(関数型エイリアス、関数を因数や戻り値で利用するためのもの)で、表示するウィジェットを生成する関数を指定する。
### showDialogの利用例
```dart
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';

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

            Padding(
              padding: EdgeInsets.all(10.0),
            ),

            Padding(
              padding: EdgeInsets.all(10.0),
              child: ElevatedButton(
                onPressed:buttonPressed,
              child: Text(
                  "tap me!",
                  style: TextStyle(fontSize:32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto"),
                )
              )
            ),
          ],
        ),
      ),
    );
  }

  void buttonPressed(){
    showDialog(
        context: context,
        builder: (BuildContext context) => AlertDialog(
          title: Text("Hello!"),
          content: Text("This is sample."),
        )
    );
  }
}
```
. . .実行することでボタンが画面に表示し、ボタンをクリックすると「Hellow!」を表示する。
## アラートにボタンを追加する
　アラートは、単にメッセージ表示をするだけではなく、さまざまな働きを用意することができる(ボタンなど)。「OK」「cancel」などのボタンを用意しクリック次第で処理を変えたりするなど。
```dart
action:<Widget>[...ウィジェットリスト...]
```
actionにはウィジェットのリストを用意し、それぞれのボタンをクリックしたときの処理を用意し、更にアラートが閉じた後の処理を用意することで、選択したボタンに応じた処理を作ることができる。またいくつかのボタンを用意するときはshowDialogのあとに「Then」を入力する
　
