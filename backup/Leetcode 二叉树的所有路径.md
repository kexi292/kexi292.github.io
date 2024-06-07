[二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/description/)
思路：维护两个链表，path和res,path记录节点的路径，res记录结果。判断每一个节点是否为叶子节点，是叶子节点就把路径转化为结果添加到res中。
问题1：
path中记录的是4，3，5，怎么快速转化为res需要的“4->3->5”。
解决：
使用String.join()
public static [String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) join([CharSequence](https://docs.oracle.com/javase/8/docs/api/java/lang/CharSequence.html) delimiter,
                          [Iterable](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html)<? extends [CharSequence](https://docs.oracle.com/javase/8/docs/api/java/lang/CharSequence.html)> elements)
例子
`List<String> strings = new LinkedList<>();
     strings.add("Java");strings.add("is");
     strings.add("cool");
     String message = String.join(" ", strings);
     //message returned is: "Java is cool"

     Set<String> strings = new LinkedHashSet<>();
     strings.add("Java"); strings.add("is");
     strings.add("very"); strings.add("cool");
     String message = String.join("-", strings);
     //message returned is: "Java-is-very-cool"`

问题2：TreeNode中的是int，路径中需要的是String,怎么快速转化
解决:path.add(root.val + "")
