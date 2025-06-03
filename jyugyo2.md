```dart
Stateクラスの利用
　StatefulWidgetについて
　　状態を扱うための機能を持っている。これは「State」というクラスとして用意されている。
 <statefulWidgetの基本形>
 class ウィジェットクラス extends StatefulWidget {
     @override                                       
     ステートクラス　createState() => ステートクラス();
 }
 <Stateクラスの基本形>
 class ステートクラス extends State<ウィジェットクラス> {
     ...略...
     @override
     Widget build(BUildContext context){
         ...略...
 StatefulWidgetはウィジェット部品(StatefulWidgetクラス)とステート部品(Stateクラス)の2つで構成。
 ウィジェットクラスは,StatefulWidgetクラスの定義。また「createState」メゾットを実装する必要がある。
 ステートクラスは、Stateクラスを継承して作成。またウィジェットクラスを「<>」で指定することで定義する
 ことができる。「build」メゾットが用意される
「createState」..ステートを作成するためのもので一般的にはステートクラスのインスタンスを作成し返す
　　　　　　　　　簡単な処理を行う。
      「build」..ステートを生成する際に呼び出されるもので、ここでステートとして表示するウィジェットを
      　　　　　　生成し返すもの。

　リスト2-3コマンド※省略
 　実行することで簡単なメッセージを表示したアプリが現れる。これはステートを使って画面に表示しているが、
 ステートを操作する処理は行っていなく「StatefulWidgetを使ったウィジェット」の意味というものをサンプル
 で表示してもの。

 ステートクラスとの連携
 　MyHomePageというウィジェットクラスをStatefulWidgetクラスとして作成して、_MyHomePageStateという
 ステートクラスを用意して、ステートとして設定する。
  @override
  _MyHomePageState createState() => _MyHomePageState();
   _MyHomePageインスタンスを作成し返している。またこの動作で_MyHomePageStateクラスがステートクラスとして
　扱われる。_MyHomePageStateクラスではbuildメゾットでScaffoldインスタンスを返し、またScaffoldでappBar
　bodyにそれぞれAppBarとTextを指定している。これによりアプリケーションバーとテキストが表示された画面が
　作成される。

　FloatingActionoButtoをクリックする。
 　リスト2-4コマンド※省略
  　実行すると右下に★マークアイコンが表示される。これをクリックすると「タップしました！」と表示する。

ステート更新とsetState
  void_setMessage(){                        このメゾットでは「setState」メゾットが実行される。
    setState((){　　　　　　　　　　　　　　ステートの更新をステートクラスに知らせる働きがある。また必要な
        _massage = 'タップしました!'；　　　 値のへんこう処理を用意する必要がある。
    ..略..
 FloatingActionButtonクラスについて
 　floatongActionButtonは「フローティングアクションボタン」と呼ばれるものを設定するためのもの。
 スマホの右下などにある、丸いアイコンを表示したボタンのこと。

 複雑の値の利用
 ここでは「Data」というクラスを定義する
　リスト2-5※省略
ここでは、MyHomePageStateクラスにDataリストを保管する_dataフィールドを用意しアイコンをクリックすると
ここからランダムなDATAを選んで表示するようにする。またDataクラスは複雑の値を扱う場合、必要な情報をまとめた
クラスとして定義するのが一般的。

