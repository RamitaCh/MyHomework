//Ramita Chongcham 6188002

      import 'package:flutter/foundation.dart';
      import 'package:flutter/material.dart' ;

      class Todo {
        final String image;
        final String title ;
        final String description;
        Todo(this.image, this. title , this .description) ;
      }

      void main() {
        var img = ['assets/images/img1.png',
          'assets/images/img2.png',
          'assets/images/img3.png',
          'assets/images/img4.png',
          'assets/images/img5.png',
          'assets/images/img6.png',
          'assets/images/img7.png',
          'assets/images/img8.png',
          'assets/images/img9.png',
          'assets/images/img10.png',
          'assets/images/img11.png',
          'assets/images/img12.png',
          'assets/images/img13.png',
        ];
        var bookTitle = ['Sherlock Holmes: A Study in Scarlet',
          'Sherlock Holmes: The Sign of the Four',
          'Sherlock Holmes: The Hound of the Baskervilles',
          'Sherlock Holmes: The Valley of Fear',
          'Sherlock Holmes: The Adventures of Sherlock Holmes',
          'Sherlock Holmes: The Memoirs of Sherlock Holmes',
          'Sherlock Holmes: The Return of Sherlock Holmes',
          'Sherlock Holmes: His Last Bow',
          'Sherlock Holmes: The Case-Book of Sherlock Holmes',
          'Hercule Poirot: The Mysterious Affair at Styles',
          'Hercule Poirot: The Mystery of the Blue Train',
          'Hercule Poirot: Murder on the Orient Express',
          'Hercule Poirot: The ABC Murders'
        ];
        var description = ['Author: Arthur Conan Doyle  |  Price: 115 THB',
          'Author: Arthur Conan Doyle  |  Price: 105 THB',
          'Author: Arthur Conan Doyle  |  Price: 135 THB',
          'Author: Arthur Conan Doyle  |  Price: 135 THB',
          'Author: Arthur Conan Doyle  |  Price: 225 THB',
          'Author: Arthur Conan Doyle  |  Price: 175 THB',
          'Author: Arthur Conan Doyle  |  Price: 235 THB',
          'Author: Arthur Conan Doyle  |  Price: 145 THB',
          'Author: Arthur Conan Doyle  |  Price: 195 THB',
          'Author: Agatha Christie  |  Price: 195 THB',
          'Author: Agatha Christie  |  Price: 185 THB',
          'Author: Agatha Christie  |  Price: 220 THB',
          'Author: Agatha Christie  |  Price: 215 THB'
        ];
        runApp(MaterialApp(
          title : 'Passing Data',
          home: TodosScreen(
                todos: List.generate(
                  13,
                  (i ) => Todo(
                    img[i],
                    bookTitle[i] ,
                    description[i],
                  ) ,
                ) ,
              ) ,
        ) ) ;
      }

      class TodosScreen extends StatefulWidget {
        final List<Todo> todos;
        List<String> bag = [];
        TodosScreen({Key key, @required this.todos}) : super(key: key);

        @override
        _TodosScreenState createState () {
          return _TodosScreenState () ;
        }
      }

      class _TodosScreenState extends State<TodosScreen> {

        @override
        Widget build(BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              title : Text('Detective Bookstore'),
            ),
            body: ListView.builder(
              itemCount: widget.todos.length,
              itemBuilder: (context, index) {
                return ListTile (
                  leading: CircleAvatar(
                    backgroundImage: AssetImage(widget.todos[index].image),
                  ),
                  title : Text(widget.todos[index]. title ) ,
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (context) => DetailScreen(todo: widget.todos[index], bag: widget.bag),
                      ),
                    );
                  },
                );
              },
            ),
            bottomNavigationBar: BottomAppBar(
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: <Widget>[
                  ElevatedButton(
                    onPressed: () {
                      _sendDataToSecondScreen(context);
                    },
                    child: Text('Finish!'),
                  ),
                ],
              ),
            ),
          ) ;
        }
        void _sendDataToSecondScreen(BuildContext context) {
          List<String> inBag = widget.bag ;
          Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => SecondPage(mybag: inBag,),
              )
          );
        }
      }

      class DetailScreen extends StatelessWidget {
        final Todo todo;
        List bag;
        DetailScreen({Key key, @required this.todo, @required this.bag}) : super(key: key);

        @override
        Widget build(BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              title : Text(todo.title ) ,
            ) ,
            body: SingleChildScrollView(
              padding: EdgeInsets.only(left: 0, right: 0, top: 20, bottom: 20),
                child: Center(
                  child: Column(
                    children: [
                      Center(
                        child: new Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          crossAxisAlignment: CrossAxisAlignment.center,
                          children: [
                            Image.asset(todo.image),
                            SizedBox(height: 10,),
                            Text(todo.title),
                            Text(todo.description),
                            SizedBox(height: 20,),
                            Row(
                              children: [
                                ElevatedButton(
                                  onPressed: () {
                                    bag.add(todo.title);
                                    Navigator.pop(context, todo.title);
                                  },
                                  child: Text('Buy This') ,
                                ),
                                ElevatedButton(
                                  onPressed: () {
                                    Navigator.pop(context) ;
                                  },
                                  child: Text('Cancel') ,
                                ),
                              ],
                            )
                          ],
                        ),
                      ),
                    ],
                  ),
                ),
            ),
          ) ;
        }
      }

      class SecondPage extends StatelessWidget {
        final List<String> mybag;
        SecondPage({Key key, @required this.mybag}) : super(key: key);

        @override
        Widget build(BuildContext context) {
          print(mybag.join(", "));
          return Scaffold(
            appBar: AppBar(
              title : Text("Second Screen"),
            ) ,
            body: new Center(
                child: new Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    crossAxisAlignment: CrossAxisAlignment.center,
                    children: [
                      Text('You have select:'),
                      SizedBox(height: 10,),
                      Text(
                          mybag.join("\n")
                      ),
                      SizedBox(height: 10,),
                      ElevatedButton(
                        onPressed: () {
                          Navigator.pop(context);
                        },
                        child: Text('Go back!'),
                      ),
                    ],
                ) ,
            ),
          );
        }
      }
