# DATA STRUCTURE - LINKEDLIST, BINARY TREE
## Linked List 
자료형을 선형적으로 묶어주는 자료형
> A linked list is a linear collection of data elements, in which linear order is not given by their physical placement in memory.
- 첫 시작 
  - head
- 마지막 번째
  - null
- 각 리스트
  - 데이터, next(다음 번 데이터 주소)

### 배열을 두고 왜 굳이?
#### Array
var myArr = [];

### Array vs Linked list
- Array
  - size
    - fixed
  - insert
    - hard
  - deletion
    - hard
  - random access
    - allowed
  - extra memory space
    - doesn't need
- Linked list
  - size
    - dynamic
  - insert
    - easy
  - deletion
    - easy
  - random access
    - not allowed
  - extra memory space
    - required

> splice : linked list의 insertion 처럼 사용된다.
> 메모리를 넉넉하게 써야 한다. : 연결리스트

### access
- array
  - 원하는 인덱스 값을 한번에 찾아올 수 있다.
    - O(1)
- linked list
  - 원하는 인덱스 값을 찾아오려면 for문을 사용해서 search를 해야한다.
    - O(n)

### linked list creation
```javascript
function LinkedList(){
    //define Node
    var Node = function(element){
        this.element = element;
        this.next = null;
    };
    
...
    
}
```
### linked list control
```javascript
function LinkedList(){
    //beneath Node

    var Node = function(element){
        this.element = element;
        this.next = null;
    };

    var length = 0;
    var head = null;
    
    this.append = function(element){
      var node = new Node(element),current;
      if(head === null){
        head = node;
      }else{
        current = head;
        while(current.next){ // current가 null일 때 까지
          current = current.next;
        }
        current.next = node; // 마지막값에 node를 넣는다.
      }
      length++;
    };

    this.insert = function(position, element){
      if(position >= 0 && position <= length){ 
        var node = new Node(element),
          current = head,
          previous,
          index = 0;

          if(position === 0){
            node.next = current;
            head = node;
          }else{
            while(index++ < position){
              previous = current;
              previous.next = node;
            }
            node.next = current;
            previous.next = node;
          }
          length++;
          return true;
      }else{
        return flase;
      }
      
    };  

    this.removeAt = function(position){
      if(position > -1 && position < length){ //linkedlist 범위 안에 있을 떄 current를 정의한다.
        var current = head,
        previos,
        index = 0;
        if(position === 0){
          head = current.next;
        }else{
          while(index++ < position){
            previous = current;
            current = current.next;
          }
          previous.next = current.next;
        }
        length--;

        return current.element;
      }else{
        return null;
      }
    };

    this.remove = function(element){
      var index = this.indexOf(element);
      return this.removeAt(index);
    };

    this.indeOf = function(element){
      var current = head,
      index = 0;

      while(current){
        if(element === current.element){
          return index;
        }
        index++;
        current = current.next;
      }
      return 
    };

    this.isEmpty = function(){
      return length === 0;
    };

    this.size = function(){
      return length;
    };

    this.toString = function(){
      string = '';

      while(current){
        string += current.element;
        current = current.next;
      }
      return string;
    };

    this.getHead = function(){
      return head;
    };
}

var link = new LinkedList();

link.append(2);
link.append(3);
link.append(5);
link.append(8);
link.append(1);

```
- append 
  - add new item to the end of the list
- insert
  - insert new item at a specified position in the list
- remove
  - removes an item from the list
- removeAt
  - removes an item from a specified in the list

## TREE
hierarhical : 구조 계층적인

### 이진 탐색 트리
부모보다 작은 값 : 왼쪽  
부모보다 큰 값 : 오른쪽  
- if root == null, node = newNode
- left child < right child
```javascript
function BinarySearchTree() {
  // 이진 탐색 트리 생성
    var Node = function(key) {
        this.key = key;
        this.left = null;
        this.right = null;
    };

    var root = null;

    // 이진 탐색 트리 삽입
    this.insert = function(key){
        var newNode = new Node(key);

        if (root === null){
            root = newNode;
        } else {
            insertNode(root, newNode);
		}
	};

    var insertNode = function(node, newNode){
        if (newNode.key < node.key){
            if (node.left === null){
                node.left = newNode;
            } else {
                insertNode(node.left, newNode);
            }
        } else {
            if (node.right === null){
                node.right = newNode;
            } else {
                insertNode(node.right, newNode);
            }
        }
    };

     this.inOrderTraverse = function(callback){
        inOrderTraverseNode(root, callback);
    };

    var inOrderTraverseNode = function(node, callback){
        if (node !== null){
            inOrderTraverseNode(node.left, callback);
            callback(node.key);
            inOrderTraverseNode(node.right, callback);
        }
    };

    function printNode(value) {
    console.log(value);
}

   this.preOrderTraverse = function(callback){
        preOrderTraverseNode(root, callback);
    };

    var preOrderTraverseNode = function(node, callback){
        if (node !== null){
            callback(node.key);
            preOrderTraverseNode(node.left, callback);
            preOrderTraverseNode(node.right, callback);
        }
    };

      this.postOrderTraverse = function(callback){
        postOrderTraverseNode(root, callback);
    };

    var postOrderTraverseNode = function(node, callback){
        if (node !== null){
            postOrderTraverseNode(node.left, callback);
            postOrderTraverseNode(node.right, callback);
            callback(node.key);
        }
    };

       this.min = function(){
        return minNode(root);
    };

    var minNode = function(node){
        if (node){
            while (node && node.left !== null){
                node = node.left;
            }

            return node.key;
        }
        return null;
    };

      this.max = function(){
        return maxNode(root);
    };

    var maxNode = function(node){
        if (node){
            while (node && node.right !== null){
                node = node.right;
            }

            return node.key;
        }
        return null;
    };

      this.search = function(key){
        return searchNode(root, key);
    };

    var searchNode = function(node, key){
        if (node == null){
            return false;
        }
        if (key < node.key){
            return searchNode(node.left, key);
        } else if (key > node.key){
            return searchNOde(node.right, key);
        } else {
            return true;
        }
    };
}
```
- preorder
  - 콜백 왼 오
- postorder
  - 왼 오 콜백
- inorder
  - 왼 콜백 오

## GULP
```bash
/gulp- imagemin : image minify/
gulp.task("imagemin", function(){
	pump([
		gulp.src(publicPath.src + 'img/*.jpg'),
		imagemin(),
		gulp.dest(publicPath.dest + 'img/')
	]);
});

/css minify(gulp-clean-css) : css minify/
gulp.task("cleancss", function(){
	pump([
		gulp.src(publicPath.src + 'css/minify.css'),
		cleancss(),
		gulp.dest(publicPath.dest + 'css/')
	]);
});

/gulp-sass : convert.scss to .css/
gulp.task("sass", function(){
	pump([
		gulp.src(publicPath.src + 'sass/*.scss'),
		sass().on('error', sass.logError),
		gulp.dest(publicPath.dest + 'css/')
	]);
});

/gulp-concat-css : concatenate css files/
gulp.task("concatcss", function(){
	pump([
		gulp.src([publicPath.src + 'css/concat1.css', publicPath.src + 'css/concat2.css']),
		concat('concatenated.css'),
		gulp.dest(publicPath.dest + 'css/')
	]);
});

/clean(del)/
gulp.task("clean", function(){
	return del.sync([publicPath.dest + 'js/*.js', publicPath.dest + 'css/*.css', publicPath.dest + 'img/']); 
});

/watch/
gulp.task("watch", function(){
	gulp.watch("public/src/*.js", ["uglify"]);
});

gulp.task("default", ["uglify", "watch"]);

/watch/
gulp.task("watch", function(){
	gulp.watch(publicPath.src + 'js/*.js', ["uglify", "concat"]),
	gulp.watch(publicPath.src + 'css/*.css', ["cleancss", "concatcss"]),
	gulp.watch(publicPath.src + 'img/*.jpg', ["imagemin"]),
	gulp.watch(publicPath.src + 'sass/*.scss', ["sass"])
 +});

```

챌린지 : [40라인으로 슬랙봇만들기](https://mager.co/how-to-write-a-slackbot-in-40-lines-of-code-52cf0c4fcf42)를 이해하고 커스터마이즈 할 수 있다면 node.js express.js heroku git REST api를 이해한것이다!!