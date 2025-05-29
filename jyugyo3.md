ウィジェットの基本レイアウト
　レイアウトの作成に関して、Flutter Studioを活用する。Webブラウザは(https://flutterstdio.app/)を使う。
 Textの配置
 　「Basic」ジャンルから「Text」アイコンをドラッグ&ドロップしてプレビュー画面に配置する。
  　配置したTextウィジェットを選択すると、右側にプロパティ表示されフォント、テキスト,Size,Weightを変えられる。
  レイアウトのソースコード
  　下のタブから「source code」に切り替えて、ソースコードをコピーしFlutterプロジェクトのmain.dartにペーストして
   ソースコードを差し替えることができる。
  　void main() {
  runApp(MyApp());
}
class MyApp extends StatelessWidget {　　　　　　これが基本となるソースコードになる。これをベースに、FLutter Studioで
  @override　　　　　　　　　　　　　　　　　　　　レイアウトを変更し、ソースコードをチェックしながら、レイアウト用のウィジェット
  Widget build(BuildContext context) {　　　　　 の使い方を学ぶ。
    return MaterialApp(
      title: 'Generated App',                   ~テキストスタイルについて~
      theme: ThemeData(　　　　　　　　　　　    テキストウィジェットを作成する際、styleという値を使って設定する。この値は、
        primarySwatch: Colors.blue,　　　　　　　「TextStyle」というクラスとして用意される。インスタンスを作成する際、必要な
        primaryColor: const Color(0xff2196f3),　　情報を因数として用意することができる。
        canvasColor: const Color(0xffafafa),　　(fontSize,fontWeight,fontFamily,fontStyle,color)
      ),
      home: MyHomePage(),　　　　　　　　　　　　　~Colorについて~
    );　　　　　　　　　　　　　　　　　　　　　　　 Colorはクラスですが、一般的に「Color~」の値。一般的に「Color~」といった形
  }　　　　　　　　　　　　　　　　　　　　　　　　　インスタンスを作成し利用することはあまりない。
}　　　　　　　　　　　　　　　　　　　　　　　　　　サンプル「color: const Color(0xff000000)」のような感じ。
                                                 「color.fromARGB(アルファ、赤、　緑、青)」ARGBの値を個別に引数で指定してインスタンス
class MyHomePage extends StatefulWidget {　　　　　を作成するメゾットも用意されている。
  MyHomePage({Key? key}) : super(key: key);　　　　　　　　　colorクラスでは色を指定するが他にもprimarySwatchのところで、Colorblue
  @override　　　　　　　　　　　　　　　　　　　　　　　　　　という値が使用される。
  _MyHomePageState createState() => _MyHomePageState();
}
　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　~テーマ指定~
class _MyHomePageState extends State<MyHomePage> {　　　　　テーマは画面表示のベースとなるウィジェットで設定する。
    @override　　　　　　　　　　　　　　　　　　　　　　　　　今回ではmyapp内で作成されるMaterialAPpインスタンスを指定する。
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(　　　　　　　　　　　　　　　　　　　　~Centerによる中央表示~
          title: Text('App Name'),　　　　　　　　　　　　中央寄せのためのウィジェットでは「center」を使用する。
          ),　　　　　　　　　　　　　　　　　　　　　　　　　表示するコンテンツを中央に寄せておけば大きさが多少変わっても見栄えよく　
        body:　　　　　　　　　　　　　　　　　　　　　　　　　同じような表記にすることができる。
          Text(
          "Hello Flutter!",
            style: TextStyle(fontSize:32.0,　　　　　　今回でaccentColor: const Color(0xFF2196f3)のようにaccentcolorをつかうと
            color: const Color(0xff000000),　エラーが発生したため、下のtheme: ThemeDataを使用することによって上のバーの色表記
            fontWeight: FontWeight.w700,　　　を落とさずできた。
            fontFamily: "Roboto"),
            
「            theme: ThemeData(
  useMaterial3: false, // Material 2 を使う場合は false にする
  primarySwatch: Colors.blue,
  primaryColor: const Color(0xFF2196f3),
  canvasColor: const Color(0xFFfafafa),
  colorScheme: ColorScheme.light(
    primary: const Color(0xFF2196f3),
    secondary: const Color(0xFF2196f3),
  ),
  appBarTheme: AppBarTheme(
    backgroundColor: const Color(0xFF2196f3), // ← ここが重要
    foregroundColor: Colors.white,
  ),
),
   」
