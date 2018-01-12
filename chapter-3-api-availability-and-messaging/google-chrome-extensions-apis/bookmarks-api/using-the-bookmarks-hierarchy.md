#### Использование иерархию закладок

Чтобы получить всю иерархию закладок используется метод `chrome.bookmarks.getTree`, который принимает единственный параметр функцию. В саму функцию передается дерево закладок виде массива.

Обратите внимание, что дерево находиться в первом элементе полученного массива. Так как дерево состоит из узлов, которые являются папками, соответственно для поиска этих папок используется свойство `children`. Чтобы пройти по всем закладкам в узле дерева можно воспользоваться методом `folder.children.forEach`.

```
chrome.bookmarks.getTree(function(bookmarkTreeAsArray) {
    var bookmarkTree = bookmarkTreeAsArray[0];
    var folders = [];
    if(bookmarkTree.children) {
        bookmarkTree.children.forEach(function(node) {
            if(node.children.length > 0) folders.push(node);
        });
    }
    if(folders.length > 0) {
        folders.forEach(function(folder) {
            folder.children.forEach(function(bookmarkTreeNode) {
                if(bookmarkTreeNode.url) {
                    /*Работа с узлом*/
                }
            }
        }
    }
});
```



