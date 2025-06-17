```dart
入力のためのUI
▼リスト3-8
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';                         TextFieldについて...
  static final _controller = TextEditingController();  |  テキストを入力するUIウィジェット。これを
　　　　　　　　　　　　　　　　　　　　　　　　　　　　　     配置することで、フォント名、カラーパレッ
  @override　　　　　　　　　　　　　　　　　　　　　　　　　 ト、Size,Weightというプロパティが表示さ
  Widget build(BuildContext context) {　　　　　　　　　　 れるようになる。
    return Scaffold(　　　　　　　　　　　　　　　　　　　　 またTextField自体は入力するためのウィ　
      appBar: AppBar(　　　　　　　　　　　　　　　　　　　  ジェットでただ表示するだけでなく、記入され
        title: Text('App Name'),　　　　　　　　　　　　　  記入されたテキストを利用する方法も理解する
      ),　　　　　　　　　　　　　　　　　　　　　　　　　　　 必要がある。
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,　　　　　　　　　　...実行すると、テキストを入力するフィ
          crossAxisAlignment: CrossAxisAlignment.stretch,　 －ルドとボタンが表示される。テキストを
          children: <Widget>[　　　　　　　　　　　　　　　　　記入し、ボタンをクリックすると、その
            Padding(　　　　　　　　　　　　　　　　　　　　　　上に「you said: ○○」というメッセージ
              padding: EdgeInsets.all(20.0),　　　　　　　　　が表示される。
              child: Text(
                _message,　　　　　　　　　　　　　　　　　　　　controllerについて...
                style: TextStyle(                           Controllerはウィジェットの値を管理
                  fontSize: 32.0,　　　　　　　　　　　　　　 するための専用のクラス。自身の中に値
                  fontWeight: FontWeight.w400,　　　　　　　 を管理するプロパティのようなものを持っ
                  fontFamily: "Roboto"),　　　　　　　　　 　ているわけではなく、値を管理するための
              ),　　　　　　　　　　　　　　　　　　　　　　　 「controll」というクラスを読み込み、
            ),　　　　　　　　　　　　　　　　　　　　　　　　 　これによって値を管理する。
            Padding(
              padding: EdgeInsets.all(10.0),
              child: TextField(
                controller: _controller,                  OnChangeedイベントの利用
                style: TextStyle(　　　　　　　　　　　　　　　ボタンをクリックした時にonPressedイベ
                  fontSize: 28.0,　　　　　　　　　　　　　　　ントで処理をしてきたが別で入力関係のウィ
                  color: const Color(0xffFF0000),　　　　　　ジェットにそれぞれ独自のイベントの
                  fontWeight: FontWeight.w400,              Onchangedがある。修正されると発生し、
                  fontFamily: "Roboto"),　　　　　　　　　　　テキストを編集している間リアルタイムに
              ),　　　　　　　　　　　　　　　　　　　　　　　　入力値を利用した処理を行わせることもできる
            ),
            ElevatedButton(
                child: Text(　　　　　　　　　　　　　　　　　
                  "Push me!",　　　　　　　　　　　　　　　　　
                  style: TextStyle(　　　　　　　　　　　　　　
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto"),
                ),
                onPressed: buttonPressed),
   　　~ 略 ~

  void buttonPressed() {
    setState(() {
      _message = 'you said: ' + _controller.text;
    });
  }
}
