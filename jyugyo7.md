# 複雑な構造のウィジェット
### AppBarについて
　AppBarは今までtitleにTextを用意することでタイトル表示を行っていた。しかしAppBarに用意されているプロパティはこれだけではない。
```dart
AppBar(
    title: ウィジェット ,
    leading: ウィジェット ,
    actions: <Widget>[ ウィジェットのリスト ],
    bottom:《PreferredSize》,
)
```
||||
|:---|:---:|---:|
|title |タイトル表示部分。通常はTextを用意|
|leading|左端に表示される。通常、ボタン化アイコンを用意|
|actions|タイトル右端に表示される。ボタン・アイコンなどのリストを用意|
|bottoM|上記の下に追加表示される部分。PreferredSizeインスタンスを用意。|
___
この中で説明が必要なのはbuttom。これは通常、特別な用途などがない限り使うことはない。使う際は、PreffedSizeというクラスを使う。これはデバイスの画面サイズなどに応じた最適なサイズを調整するためのものでこの中にウィジェットを食い込んで表示させる。

### BackButtonについて
```dart
leading:BackButton(
    color: Colors.White,
),
```
ここで使用している「BackButton」は「前に戻る」ための専用ボタン。今回は表示を移動したりしていないため、必要ないが一般的にleadingに配置されるウィジェットとして作成している。
### actionsのアイコンについて
```dart
actions:<Widget>[
    IconButton(
        icon: Icon(Icons.android),
        tooltip: 'add star...',
        onPressed: iconPressedA,
    ),
    ...略...
],
```
actionsはおそらくAppBarで最も活用される部分。
今回は、IconButtonインスタンスを用意した。actionsは、タイトルの右側の限られたエリアに表示するもののため、アイコンなど小さいスぺースで表示内容がわかるものを使う。onPressedでクリック時の処理を用意する。

### BottomNavigationBarについて
Scaffoldでは、AppBarのように画面に表示する上部だけではなく、下部にもバーを表示することを「ButtomNavigationBar」で可能としている。
Scaffoldには、「bottomNavigationBar」という値が用意されている。これにBottomNavigationBarクラスのインスタンスを設定することで、下部のバーを表示できる。またBUttomNavigationBarには,BottomNavigationBarItemというウィジェットをを組み込むことでアイコンを表示し、クリックすることで操作をすることもできる。
### BottomNacigationBar利用例
```dart
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok';
  static var _index = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Text(
          _message,
          style: const TextStyle(
            fontSize: 28.0,
          ),
        )
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _index,
        backgroundColor: Colors.lightBlueAccent,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'Android',
            icon: Icon(Icons.android,color: Colors.black, size: 50),
          ),
          BottomNavigationBarItem(
            label: 'Favorite',
            icon: Icon(Icons.favorite,color: Colors.red, size: 50),
          ),
          BottomNavigationBarItem(
            label: 'Home',
            icon: Icon(Icons.home,color: Colors.white, size: 50),
          ),
        ],
        onTap: tapBottomIcon,
      ),
    );
  }

  void tapBottomIcon(int value) {
    var items = ['Android', 'Heart', 'Home'];
    setState(() {
      _index = value;
      _message = 'you tapped: "' + items[_index] + '".';
    });
  }
}
```
. . .実行すると下部に３つのあいこんを表示したバーが現れる。これが、BottomNavigationBar。アイコンをクリックすると、そのアイコンが選択され、「you tapped: ○○」というメッセージが表示される。
### BottomNavigationBarの仕組み
このBottomNavigationBarを利用するためには
、ある程度の仕組み理解が必要とされる。ただアイコンやボタンを追加してイベント処理を書けばいいというわけではない。
```dart
BottomNavigationBar(
    currentIndex:《int値》,
    items: <BottomNavigationBarItem>[リスト],
    onTap: 関数
)
```
||||
|:---|:---:|---:|
|currentIndex|現在、選択されている項目のインデックス。これに設定されたインデックスのアイコン(BottomNavigationBarItem)が選択状態で表示される。 |
|items|表示する項目。ButtomNavigationBarItemインスタンスのリストとして用意。|
|onTap|バーに表示されるアイコンをクリックしたときに呼び出される処理|
___
ButtomNavigationBarはいくつかのアイコンを表示するが、これは一般的なボタンやアイコンとは少し働きが違う。一般的なボタン類は、それぞれのボタンにonPressedイベントが用意されていて個別に処理が用意されている。しかしButtomNavigationBarに組み込まれるButtomNavigationBarItemにはない。
そのためアイコンを組み込んでいるButtomNavigationBar側にイベント処理を設定する。
```dart
void メゾット (int value) {...}
```
引数に、int値が渡される。またクリックした項目のインデックス番号のことを指す。この番号によって、何番目の項目がクリックされたかをチェックし、処理を行う。
アイコンのサイズ、カラーには以下を使う
```
Icon(Icons.android,color: Colors.black, Size: 50)
```
color引数にColorを指定することでアイコンの色を変更できる。またSizeにdouble値を指定することで、アイコンの大きさを指定できる。

### ListViewについて
ListViewは、リストを表示するためのウィジェット。リストは、スマートフォンのシステムの設定など多数の項目を並べて表示するようなところでよくみられるインターフェース。
今回ではFlutter Studioの「Scrollig」というジャンルで用意されている。ListViewをドラッグ&度ラップで配置すると、上下左右のスペースを調整するプロパティが表示される。ListViewには、表示する項目などのプロパティがあるが、これらには特に用意されておらず、自分でコーティングする必要がある。
### ListViewの使用例
```dart
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),

      body: Column(
        children: <Widget>[
          Text(
            _message,
            style: TextStyle(
              fontSize: 32.0,
            ),
          ),

          ListView(
            shrinkWrap: true,
            padding: const EdgeInsets.all(20.0),

            children: <Widget>[

              Text('First item',
                style: TextStyle(fontSize: 24.0),
              ),
              Text('Second item',
                style: TextStyle(fontSize: 24.0),
              ),
              Text('Third item',
                style: TextStyle(fontSize: 24.0),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
```
```dart
ListView(
    shrinkWrap:《bool値》,
    padding:《EdgeInsets》,
    children:<Widget>[リスト],
)
```
ShrinkWrapは、追加された項目に応じた大きさを自動調整するための設定。trueにすると表示項目に応じて大きさが自動調整される。
リストに表示される項目は,childrenに用意する。これはウィジェットリストだが、今回はTextを複数用意されている。

### ListTileで項目を用意する
ListViewの表示された項目をクリックして操作するなどの使い方をするならば、ListWiew用に用意されている専用のウィジェット「ListTile」を使う。
```dart
ListTile(
    leading:《Icon》,
    title: ウィジェット,
    selected:《bool値》,
    onTap: 関数,
    onLongPress: 関数
)
```
||||
|:---|:---:|---:|
|leading|項目の左端に表示するアイコン。Iconインスタンスでしてする。|
|title|項目に表示する内容|
|selected|その項目の選択状態。trueならば選択されている。|
|onTap|クリックされた際のイベント処理。|
|onLongPress|ロングクリックされた際のイベント処理。|
___
### ListTileの利用例
```dart
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _index = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(

      appBar: AppBar(
        title: Text('My App'),
      ),

      body: Column(
        children: <Widget>[
          Text(
            _message,
            style: TextStyle(
              fontSize: 32.0,
            ),
          ),
          ListView(
            shrinkWrap: true,
            padding: const EdgeInsets.all(20.0),
            children: <Widget>[

              ListTile(
                leading: const Icon(Icons.android, size:32),
                title: const Text('first item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 1,
                onTap: () {
                  _index = 1;
                  tapTile();
                },
              ),

              ListTile(
                leading: const Icon(Icons.favorite, size:32),
                title: const Text('second item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 2,
                onTap: () {
                  _index = 2;
                  tapTile();
                },
              ),

              ListTile(
                leading: const Icon(Icons.home, size:32),
                title: const Text('third item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 3,
                onTap: () {
                  _index = 3;
                  tapTile();
                },
              ),
            ],
          ),
        ],
      ),
    );
  }

  void tapTile() {
    setState(() {
      _message = 'you tapped: No, $_index.';
    });

  }
}
```
. . .実行すると、アイコンが表示されたリストの項目が3つ表示される。これらがListTileによる項目。クリックするとその項目が選択され、上に「you tapped: No,○○」とクリックした項目の番号が表示される。
### Listtileの基本形
```dart
ListTile(
    leading: const Icon(Icons.android, size:32),
    title: const Text('first item',
       style: TextStyle(fontSize: 28)),
    selected: _index == 1,
    onTap: () {
        _index = 1;
        tapTile();
    },
),
```
leaddingでは、Iconインスタンスを作成し設定している。これはconst Iconで作成し、引数にIcons.android,size32を指定している。titleにはテキストの設定をする。
選択状態を示すselectedは、_indexとこのListTileに割り当てた番号が等しいかどうかをチェックした結果を代入している。selected: _index == 1では、_indexの値が1ならtrueとなり選択された状態になるというようなもの。またこの動作により特定の項目だけを選択できるようになる。
onTapでは_indexの値を設定した後tapTileメゾットを呼び出している。またsetStateを呼び出して表示を更新している。

### singleChildScrollViewについて
singleChildScrollviewは名前の通り、一つのウィジェットを内部にもてるコンテナで、そのウィジェットの幅に応じた自動的にスクロールを表示することができる。
