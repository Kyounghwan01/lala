---
layout: post
title: "수식 트리, expression tree"
date: 2018-08-05
excerpt: "수식 트리를 만드는 방법"
tag:
- Datastructure
- Algorithm
category: [ Algorithm ]
feature: https://png93.github.io/assets/img/title/lego.jpg
comments: true
---

_『뇌를 자극하는 알고리즘』 을 바탕으로 공부한 내용입니다._
{: .notice}

## 수식 트리
수식을 표현하는 이진 트리.
<br>
루트 노드와 가지 노드들은 양쪽 자식으로 피연산자를 가진다. Leaf 노드는 모두 피연산자이며 수(Number) 이다.
<br>

수식트리는 '후위순회'를 통해 계산결과를 병합해 올라가며 연산을 수행.

## 수식 트리 구축

1. 후위 표기식 __뒤에서__ 부터 읽기. <br>
후위 표기식을 뒤에서 부터 읽어서, 맨 처음 토큰이 루트 노드가 되고 그 다음 토큰을 계속해서 읽으면서 연산자이면 양쪽 자식을 만들어준다.
<br>
위와 같은 방식으로 C언어 코드를 작성 하였는데, java 코드로 변경하는 데 어려움을 겪어서.. 아래 방법을 사용.
<br>

2. 후위 표기식 __앞에서__ 부터 읽기. <br>
후위 표기식을 앞에서 부터 읽으면서 규칙에 따라 스택에 담는 방법.

- 피연산자이면, 노드를 만들어 스택에 쌓는다.
- 연산자이면, 스택에서 노드 두개를 pop한 후
첫 번째 노드는 연산자의 오른쪽, 두 번째 노드는 왼쪽 자식으로 만든다. 이렇게 만들어진 연산자 노드를 스택에 쌓는다.
- 식을 모두 읽을 때 까지 반복한다.
<br>

(참고한 블로그)
[수식 트리의 구현](http://blog.naver.com/PostView.nhn?blogId=muramura12&logNo=220704218849&redirect=Dlog&widgetTypeCall=true)


<br><br>

ExpressionTree.java
~~~java
package data_structure.tree;

import java.util.Stack;

/*
 * 수식 트리 구축, 계산, 출력 구현
 *	- 수식은 후위표기식으로 입력되며 연산자와 피연산자들은 공백 하나로 구분된다고 가정.
 */

public class ExpressionTree {

	public static class Node<E>{
		E data;
		Node<E> left;
		Node<E> right;
		public Node(E data) {
			this.data = data;
			left = null;
			right = null;
		}
	}

	/*
	 * <수식트리 구축>
	 *
	 * 후위 표기식을 앞에서부터 읽어가면서,
	 * 1. 토큰이 연산자인 경우 스택의 최상위 노드 두개를 꺼내 순서대로 연산자 노드의 오른쪽, 왼쪽 자식으로 만든다.
	 * 2. 토큰이 피연산자(숫자)인 경우 노드를 만들어 스택에 담는다.
	 *
	 * 위 과정을 수식을 다 읽을 때 까지 반복한다.
	 *
	 * "모든 과정 완료 후에 스택에는 루트노드에 대한 정보만 남아 있게 된다."
	 */
	public Node<String>  build(String expression) {

		String[] postfix = expression.split(" ");
		Stack<Node<String>> treeStack = new Stack<>();

		for (int i = 0; i < postfix.length; i++) {

			String token = postfix[i];

			switch (token) {
			case "+": case "-": case "*":case "/":

				Node<String> newnode = new Node<String>(token);

				newnode.right = treeStack.pop();
				newnode.left = treeStack.pop();

				treeStack.push(newnode);

				break;

			default:
				//피연산자인 경우
				treeStack.push(new Node<String>(token));

				break;
			}

		}

		return treeStack.peek();

	}


	//트리 출력 (후위순회)
	public void postorder(Node<String> node) {
		if(node == null)
			return;

		postorder(node.left);
		postorder(node.right);
		System.out.println(node.data);
	}

	/*
	 * <수식 트리 계산>
	 * 노드의 데이터가 연산자인 경우, 재귀호출을 통해서 해당 연산자 결과 값을 얻는다.
	 * 따라서, 피연산자인 Leaf노드에 도달할 때 까지 재귀호출이 반복된다.
	 */
	public double evaluate(Node<String> node) {

		double left = 0;
		double right = 0;

		if(node == null)
			return 0;

		switch (node.data) {
		case "+": case "-": case "*": case "/":

			left = evaluate(node.left);
			right = evaluate(node.right);

			if(node.data.equals("+")) {
				return left + right;
			} else if(node.data.equals("-")) {
				return left - right;
			} else if(node.data.equals("*")) {
				return left * right;
			} else if(node.data.equals("/")) {
				return left / right;
			}

		default:

			return Double.parseDouble(node.data);
		}

	}
~~~

<br>

ExpressionTreeMain.java

{% highlight java %}
package data_structure.tree;

import data_structure.tree.ExpressionTree.Node;

public class ExpressionTreeMain {

	public static void main(String[] args) {

		ExpressionTree et = new ExpressionTree();

		String expression = "7 1 * 5 2 - /";

		Node<String> root = et.build(expression);

		System.out.println("<수식트리 후위 순회 출력>");
		et.postorder(root);

		System.out.println("\n<수식트리 계산 결과>");
		System.out.println(et.evaluate(root));
	}

}
{% endhighlight %}

<br>

출력결과
~~~
<수식트리 후위 순회 출력>
7
1
*
5
2
-
/

<수식트리 계산 결과>
2.3333333333333335
~~~
