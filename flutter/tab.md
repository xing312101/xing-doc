# tab

## DefaultTabController include app scaffold
```
DefaultTabController(
      length: 2,
      child: Scaffold(
        drawer: MainDrawer(),
        appBar: AppBar(
          actions: [
            _actionButtons()
          ],
          bottom: TabBar(
            tabs: [
              Tab(text: 'tab1'),
              Tab(text: 'tab2')
            ],
          ),
          title: Center(child: Text('hello world')),
        ),
        body: TabBarView(
          children: [
            Icon(Icons.directions_car),
            Icon(Icons.directions_transit),
          ],
        )
      )
    );
```


## DefaultTabController in app scaffold body
```
Scaffold(
        drawer: MainDrawer(),
        appBar: AppBar(
          actions: [
            _actionButtons()
          ],
          title: Center(child: Text('title')),
        ),
        body: DefaultTabController(
            length: 2,
            child: Column(
              children: [
                TabBar(
                  labelColor: Colors.black,
                  tabs: [
                    Tab(text: 'tab1'),
                    Tab(text: 'tab2')
                  ],
                ),
                Expanded(
                  child: TabBarView(
                    children: [
                      CmRecord(),
                      CmHistory(),
                    ],
                  ),
                )
              ],
            )
        )
    );
```


## bottom tab
```
int _currentIndex = 0;
  final pages = [
    Form1(),
    Form2(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.
        title:
        actions: [
        ]
      ),
      body: pages[_currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        fixedColor: Colors,
        selectedLabelStyle: TextStyle(),
        selectedFontSize: 18,
        unselectedFontSize: 14,
        showSelectedLabels: true,
        showUnselectedLabels: true,
        iconSize: 0,
        items: [
          BottomNavigationBarItem(
              backgroundColor: Colors.,
              icon: Icon(Icons.add),
              label: 'form one'
          ),
          BottomNavigationBarItem(
              backgroundColor: Colors.,
              icon: Icon(Icons.add),
              label: 'form 2'
          ),
        ],
        currentIndex: _currentIndex,
        onTap: _onButtomNavigationBarClick
      ),
    );

  }
```
