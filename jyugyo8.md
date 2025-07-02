# ナビゲーションとルーティング
### 表示切替とナビゲーション
ナビゲーション機能とは「Navigator」というクラスとして用意されている。この機能は以下の動きを指す。  
  
  **・移動先のウィジェットを追加すると、そのウィジェットに表示を切り替える。**  
  **・保管されたウィジェットを取り出すと、そのウィジェットに表示を戻す。**  

  「追加する」「取り出す」などのコレクション的機能と表示の切り替えが一体化したようのもので2つのメゾットが用意されている。  
  #### ■移動先をプッシュする
  ```dart 
  Navigator.push(《BuildContext》,《Route》); 
  ```
  #### ■移動をポップする
  ```dart
  Navigator.pop(《BuildContext》);
  ```
  Navigatorのpushは、現在の表示をプッシュ（データを保管する）し、起動先に表示を切り替える働きをする。そしてpopは、最後に保管した移動元をポップ（取り出す）し、そこに表示を戻す。  
  push = 移動,pop = 戻る

  ### Navigatorで移動する
  ```dart
  import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: const Color(0xfffafafa),
      ),
      home: FirstScreen(),
    );
  }
}

// １つ目のスクリーン
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Home'),
      ),
      body: Center(
        child: Container(
          child: const Text('Home Screen',
              style: const TextStyle(fontSize: 32.0)),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'Home',
            icon: const Icon(Icons.home, size:32),
          ),
          const BottomNavigationBarItem(
            label: 'next',
            icon: const Icon(Icons.navigate_next, size:32),
          ),
        ],
        onTap: (int value) {
          if (value == 1)
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context)=>SecondScreen()),
            );
        },
      ),
    );
  }
}

// ２つ目のスクリーン
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Next"),
      ),
      body: Center(
        child: const Text('Next Screen',
            style:const TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before, size:32),
          ),
          const BottomNavigationBarItem(
            label: '?',
            icon: const Icon(Icons.android, size:32),
          ),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
        },
      ),
    );
  }
}
```
...実行することで「Home Screen」と表示された画面が現れる。下にはナビゲーションバーがあり、「home」「next」というアイコンが表示される。「next」アイコンがクリックすると、「Next Screen」と表示されウィジェットに切り替わる。
また左下の「prev」アイコンをクリックすると、元の「Home Screen」に表示が戻る。

### MaterialPageRouteについて
```dart
Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondScreen());
);
```
Navigatirは、画面表示を切り替える機能を提供するが、この表示の切り替えは「ある画面から別の画面に移動する」という形で扱われる。画面の表示に関する情報は「Route」というクラス（サブクラスより）で管理されている。ここでは**Route**のサブクラスである**PageRoute**およびそのサブクラス**MaterialPageRoute**を使っている。このクラスは現在表示をそのままPageRouteクラスのインスタンスに置き換えて記録する働きをする。  
またここでは、Navigator.pushを呼び足している。また第一因数には、contextを指定している。第二因数には、MaterialPageRouteクラスのインスタンスを設定している。

### 表示間の値の受け渡し
**サンプルを修正する**  
考え方としては簡単だが実際に実装する場合、イメージのつきにくいためサンプルを修正し、FirstScreenで入力した値をSecondScreenに渡して表示するようにFirst,SecondScreenを修正する
```Dart
class FirstScreen extends StatefulWidget {
  FirstScreen({Key? key}) : super(key: key); // コンストラクタ

  @override
  _FirstScreenState createState() => _FirstScreenState();
}

class _FirstScreenState extends State<FirstScreen> {
  static final _controller = TextEditingController();
  static var _input = '';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Column(
        children: <Widget>[
          const Text('Home Screen',
          style: const TextStyle(fontSize: 32.0)),
          Padding(
            padding: const EdgeInsets.all(20.0),
            child: TextField(
                controller: _controller,
                style: const TextStyle(fontSize: 28.0),
                onChanged: changeField,
              ),
          ),
        ],
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'Home',
            icon: const Icon(Icons.home),
          ),
          const BottomNavigationBarItem(
            label: 'next',
            icon: const Icon(Icons.navigate_next),
          ),
        ],
        onTap: (int value) {
          if (value == 1) {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen(_input)),
            );
        }
      },
    ),
    );
  }

  void changeField(String val) => _input = val;
}

class SecondScreen extends StatelessWidget {
  final String _value;

  SecondScreen(this._value);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Next"),
      ),
      body: Center(
        child: Text(
          'you typed: "$_value".',
          style: const TextStyle(fontSize: 32.0),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before),
          ),
          BottomNavigationBarItem(
            label: '?',
            icon: const Icon(Icons.android),
          ),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
        },
      ),
    );
  }
}
```
...実行することで入力フィールドを持つ画面が現れる。ここにテキストを記入してから、右下の「next」アイコンがクリックすると、Second Screenに移動し、「you type:"○○"」と入力したテキストが表示される。  
   

#### テキストの受け渡しの流れ
ここではテキストを入力するため、First ScreenはStatefukWidgetにし、FirstScreenStateクラスを新たに定義して画面の表示を作成している。TextFieldのコントローラーとしてTextEditingControllerを作成し、TextFieldのonChangedで入力されたテキストを_inputというフィールドに保管されています。NavigatorでSecondScreenに移動するpushメゾットでは以下のように引数を用意する。
```dart
MaterialPageRoute(builder:(context) => SecondScreen(_input))
```
SecondScreen(_input)という具合に,_inputを引数に指定している。このSecondScreen側では、以下のようにしてコンストラクタを用意する
```
SecondScreen(this._value);
```
これで、_inputがそのまま_valueプロパティに代入される。

### テキストによるルーティング
あらかじめルートを表示するウィジェットの関係を定義し、ルートの値を設定することで指定のウィジェットを表示したりすることで値や変数を使って移動先のルートを指定できるようになるっといった「routes」というプロパティを使う。
```dart
routes:{
  'アドレス':(context) => ウィジェット,
  'アドレス':(context) => ウィジェット,
  .....必要なだけ記述.....
}
```
アドレスと関数を必要なだけroutes内に用意しておく。また、あらかじめアドレスと移動先のウィジェットをroutesに定義しておくことで、指定のアドレスがpushされたらそのウィジェットを表示するなどの形で処理を行うことができる。

### routesによるルーティング
```dart
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: const Color(0xfffafafa),
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => FirstScreen(),
        '/second': (context) => SecondScreen('Second'),
        '/third': (context) => SecondScreen('Third'),
      },
    );
  }
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child:const Text('Home Screen',
          style: const TextStyle(fontSize: 32.0),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'Home',
            icon: const Icon(Icons.home),
          ),
          BottomNavigationBarItem(
            label: 'next',
            icon: const Icon(Icons.navigate_next),
          ),
        ],
        onTap: (int value) {
          if (value == 1)
            Navigator.pushNamed(context, '/second');
        },
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  final String _value;
  SecondScreen(this._value);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Next"),
      ),
      body: Center(
        child: Text(
          '$_value Screen',
          style: const TextStyle(fontSize: 32.0),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before),
          ),
          BottomNavigationBarItem(
            label: '?',
            icon: const Icon(Icons.android),
          ),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
          if (value == 1)
            Navigator.pushNamed(context, '/third');
        },
      ),
    );
  }
}
```
...実行することで右下のアイコンをクリックして時にFirst ScreenからSecond Screenへ、更にThird Screenへと表示が変わる。

#### routesの定義
```dart
routes:{
  '/':(context) => FirstScreen(),
  '/second':(context) => SecondScreen('second'),
  '/third':(context) => SecondScreen('Third'),
},
```
ここでは、'/'というアドレスにFirstScreen,'/second'にSecondScreen,'/third'にSecondScreen(引数違い)を割り当てている。表示するウィジェットにアドレスを割り当てることで、そのアドレスの値で指定のウィジェットに表示をが切り替えられるようになる。
```dart
initialRoute: '/',
```
起動時に最初に表示されるウィジェットを指定するもので、'/'を指定することでFirstScreenが表示されるようになる。routesを利用する場合は、homeプロパティは利用しなく、必ずinitialRouteで起動用のアドレスを指定する。

#### pushNamedによる表示移動
routesを利用する場合、ページの井戸はNavigatorのpushを使わない。「pushNamed」というメゾットを使う。
```dart
Navigator.pushNamed(
  context,
  '/second',
);
```
pushNamedは、引数にBuildContextとアドレスの値(String)を指定する。また指定のアドレスをroutesから検索し、それに割り当てられたウィジェットに表示が切り替わる。pushNamed部分の記述がシンプルになった分だけ、実際の移動が変わりやすくなる。そして、ウィジェットの設定などを変更してアクセスするような場合も設定ごとに異なるアドレスを割り当てることで移動を整理しやすくする。