```dart
プロジェクトの構成
アプリ画面とウィジェットツリー
ウィジェット…flutterの画面表示を作成する部品。ボタンのように画面で見え操作できるようなものもあれば、
　　　　　　 決めたレイアウトを配置する見えないウィジェットもある。
ウィジェットツリー…ウィジェットを階層的に組み込んで作成する組み込み構造。
アプリの組み込み…
   void main (){                main関数がアプリを起動する際に呼び出される処理。　　　　　　
    runApp(ウィジェット)；　　　　ここではrinAppという関数を定義し「main関数で,runAppでアプリ    
   }　　　　　　　　　　　　　　　　を起動する」という意味となる。
 
 StatelessWidgetクラスについて
 　MyAppというクラスのインスタンス「StatelessWidget」というサブクラスがある。
 StatelessWidgetはステート(状態を表す値)を持たないウィジェットのベースとなるクラスである。

 MaterialAppクラス
  引数にさまざまな設定情報を指定することができる。
  return MaterialApp( title: ○○, home: ○○);
    ここではtitleはアプリケーションタイトル名、homeがこのアプリケーションのウィジェットを示す。
    またこの全体がMaterialAppの表示となる。
  Textウィジェット
  　「Text」というクラスのインスタンスで指定される。これはテキストの表示を行うためのウィジェット。
  引数には、第一引数に表示されるテキストが指定される。

  マテリアルデザイン
  　マテリアルデザインは、Googleが提唱する視覚的デザイン言語。スマートフォンだけにとどまらず
  あらゆるデバイスで共通したルック＆フィールを構築し、同じユーザ体験を実現するものとして提唱
  されている。
  Flutterでは標準的ウィジェットは、すべてwidget.dartというパッケージにまとめられてデフォルトで
  読み込め使われるようになっている。

  ScaffoldとAppbar
   スマートフォンのアプリなど上部にタイトル表示をするアプリケーションバー、またUI表示に使われる。
  import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}
class MyApp extends StatelessWidget {　　これを実行すると、上部にアプリケーションバーが配置され、
  @override　　　　　　　　　　　　　　　　　そこに「Hello World!」とタイトル表示をする。
  Widget build(BuildContext context) {　　またその下のエリアに「Hello Flutter WOrld!」
      return MaterialApp(　　　　　　　　　というテキスト表記をする。
      title: 'Flutter Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello Flutter!'),　
        ),
        body: Text(
          'Hello Flutter World!!',
          style: TextStyle(fontSize:32.0),
　　　~略~
Scaffoldについて
　Scaffoldはいわば「足場」という意味を果たす。アプリ作成の土台をなる部分を担当する部品。
マテリアルデザインの基本的なデザインとレイアウトが組み込まれている。またこれと必要な
ウィジェットを追加することで一般的なデザインのアプリが作成される。
　※ Scaffold( appBar:○○ , body:○○　)など

