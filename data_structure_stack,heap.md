# 자료구조 - stack, heap

## 자료구조 in Web development
Array & Hash(dictionary) - indexing post
```sql
in RDB
[articleId, title, body, userId, view]
[{
	userId: 1,
	articleId: 1,
	view: 100,
	title: "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
	body: "quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto"
}, 
...

]
```

Tree - Dom rendering performance, reply
```html
<html>
<head></head>
<body>
<h1></h1>
<p></p>
</body>
</html>
```
- binary Tree Search
  - Queue(BFS, Breadth First Search) : 넓이 탐색
  - Stack(DFS, Depth First Search) : 깊이 탐색

- Stack
  - array를 먼저 선언
  - push & pop
    - push : prametor 로 array에 push
```javascript
//Create Stack class
function Stack() {
	//properties, methods
	var items = [];
}

//push & pop
function Stack() {
	//properties, methods
	var items = [];

	this.push = function(element){
		return items.push(element);
	};


	this.pop = function(){
		return items.pop();
	};
}

//peek & isEmpty
function Stack() {
	//underneath push & pop
    
...
    
	this.peek = function(){
		return items[items.length-1];
	};
	this.isEmpty = function(){
		return items.length == 0;
	};
	

}
```