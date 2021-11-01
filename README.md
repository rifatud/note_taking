import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() => runApp(NoteTakingApp());

class NoteTakingApp extends StatelessWidget {
  const NoteTakingApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyNoteHome(),
    );
  }
}

class MyNoteHome extends StatefulWidget {
  const MyNoteHome({Key? key}) : super(key: key);

  @override
  _MyNoteHomeState createState() => _MyNoteHomeState();
}

class _MyNoteHomeState extends State<MyNoteHome> {
  List<Map> myNotes = [
    {"title": "Title 1", "text": "this is text 1"},
    {"title": "Title 2", "text": "this is text 2"},
    {"title": "Title 1", "text": "this is text 1"},
    {"title": "Title 2", "text": "this is text 2"},
    {"title": "Title 1", "text": "this is text 1"},
    {"title": "Title 2", "text": "this is text 2"},
    {"title": "Title 1", "text": "this is text 1"},
    {"title": "Title 2", "text": "this is text 2"},
  ];

  TextEditingController titleController = TextEditingController();
  TextEditingController textController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: () => showDialog(
          context: context,
          builder: (context) => AlertDialog(
            title: Text("Add Note"),
            content: SingleChildScrollView(
              child: Column(
                children: [
                  Text("Title"),
                  TextField(
                    controller: textController,
                  ),
                  Text("Text"),
                  TextField(
                    controller: textController,
                  ),
                ],
              ),
            ),
            actions: [
              ElevatedButton(
                onPressed: () {
                  setState(() {
                    String noteTitle = titleController.text.trim();
                    String noteText = textController.text.trim();

                    Map newData = {
                      "title" : "$noteTitle",
                      "text" : "$noteText",
                    };
                    myNotes.add(newData);
                  });
                },
                child: Text("add"),
              ),
            ],
          ),
        ),
      ),
      appBar: AppBar(
        title: Text("Note Taking App"),
      ),
      body: Container(
        height: double.infinity,
        width: double.infinity,
        child: GridView.builder(
          itemCount: myNotes.length,
          gridDelegate:
              SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 2),
          itemBuilder: (context, i) => Card(
            child: GridTile(
              header: Text(myNotes[i]["title"],
                  style: TextStyle(color: Colors.black)),
              child: Container(
                padding: EdgeInsets.fromLTRB(0, 30, 0, 0),
                child: Text(myNotes[i]["text"],
                    style: TextStyle(color: Colors.black)),
              ),
              footer: Text("GridTile footer",
                  style: TextStyle(color: Colors.black)),
            ),
          ),
        ),
      ),
    );
  }
}
