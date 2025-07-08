# タブビューとドロワー
### TabBarとTabBarView
タブのUIを作成するのに用意されるのが「**TabBar**」と「**TabBarView**」。
これらのプロパティは、現状ではAlignmentとSize関係のものが３つ表示されるだけで、タブ特有のプロパティは用意されていない。そのため生成されたソースコードをもとにコードを追記して作成しなければならない。
#### TabBarの基本形
TabBarは、タブの切り替え,ノブの部分の表示をするUIウィジェット。これは通常,AppBarの「bottom」にインスタンスを設定する。
```dart
TabBar(
    controller:《TabController》,
    tabs:[tabロスト],
),
```
controllerに「TabController」というクラスのインスタンスを設定する。これはタブ操作の制御を担当する部分でこのTabControllerをTabBarとTabBarViewの両方に設定することで両者の操作を連動することができる。
tabsにはタブをクリックするノブの部分のウィジェットとして、「Tab」クラスのインスタンスをリストにまとめて渡す。

#### TabBarViewの基本形
```dart
TabBarView(
    controller:《TabController》,
    children:[ウィジェットのリスト],
)
```
controllerには、TabBarに設定したTabControllerを指定する。またchildrenには、このタブに表示されるコンテンツをリストとして用意し、これでタブの表示全体が作成される。

#### TabControllerについて
```dart
TabController(
    vsync:《TickerProvider》,
    length:《int値》,
)
```
vsyncは、TickerProviderというクラスのインスタンスを設定する。これはアニメーションのコールバック呼び出しに関するTickerというクラスを生成するためのものでこれを引数に指定することでTabBarとTabBarViewの動きが連動できるようになる。lengthはタブの数を表す。このほか、initialIndexという値で初期値の状態を指定できる。

#### Tabクラスについて
