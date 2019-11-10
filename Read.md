# 리스트, 트리 및 그래프 자료구조

### 리스트

![](https://dojang.io/pluginfile.php/708/mod_page/content/14/unit74-1.png)

리스트란 데이터가 들어올때 마다 동적으로 메모리를 할당하는 자료 구조 이고 노드안에 들어있는 데이터 필드와 링크라는 변수의 모습에 따라 단일 연결리스트(Singly Linked List), 이중 연결리스트(Doubly Linked List), 환형 연결리스트(Circular Linked List)로 구분된다.

### 리스트의 종류

단일 연결리스트(Singly Linked List) - 노드당 링크가 하나밖에 없어서 이전 노드로 갈 수 없는 번거로움이 있는 리스트

이중 연결리스트(Doubly Linked List) -  단일 연결리스트에서 이전 노드로 갈 수 있는 링크를 하나 더 추가한 리스트

환형 연결리스트(Circular Linked List) - 마지막 노드가 첫번째 노드를 가르켜서 계속 회전할 수 있게 만들어진 리스트

### 예제 코드

```
#include <stdio.h>
#include <stdlib.h>
typedef struct NODE{
	int data;
	struct NODE* next;
}node;
int main(void) {
	node* head = (node*)malloc(sizeof(node));
    head->next=NULL;
    node* node1 = (node*)malloc(sizeof(node));
	node1->next = head->next;
	node1->data = 10;
	head->next = node1;
	node* node2 = (node*)malloc(sizeof(node));
	node2->next = node1->next;
	node2->data = 20;
	node1->next = node2;
	node* curr = head->next;
	while(curr != NULL){
		printf("%d\n", curr->data);
		curr = curr->next;
	}
	free(head);
	free(node1);
	free(node2);
	return 0;
}
```

***

### 트리

![](http://2.bp.blogspot.com/-m-c-4PgDLUI/VO1EPmAoSJI/AAAAAAAAAuY/ov1rknsdcts/s1600/%ED%8F%AC%ED%99%94%EC%9D%B4%EC%A7%84%ED%8A%B8%EB%A6%AC.PNG)

트리는 자신이 가르키는 데이터가 1개가 아닐수도 있는 구조이며 이것은 선형구조와의 결정적인 차이점이다. 그리고 트리구조는 계층 구조를 가진다.
자식 노드가 2개 오는 트리를 이진 트리(Binary Tree), 자식이 3개 오는 삼진 트리(Ternary Tree)가 있는데 주로 이진 트리(Binary Tree)를 사용한다.

### 이진 트리의 종류

이진 트리(Binary Tree) - 다른 조건없이 노드에 자식이 최대 두개씩 붙어있는 트리

이진 검색 트리(Binary Search Tree) - 왼쪽 노드와 그 이하 자식은 현재 노드보다 작고 오른쪽 노드와 그 이하 자식은 현재 노드보다 큰 데이터를 가지는 트리

완전 이진 트리(Complete Binary Tree) - 마지막 레벨을 제외하고 모든 레벨에 노드가 다 채워지고 잎 노드들이 왼쪽부터 오른쪽으로 순서대로 채워지는 트리

포화 이진 트리(Full Binary Tree) - 잎 노드를 제외한 모든 부모 노드가 자식을 2씩 갖는, 모든 잎노드의 높이가 같은 트리

Perfect Binary Tree - 모든 노드의 자식 노드 개수가 2개이고 잎 노드들의 레벨이 모두 같은 트리

### 예제 코드

```
#include <stdio.h>
#include<stdlib.h>
#include<memory.h>
typedef struct treeNode {
	char data;
	struct treeNode* left;
	struct treeNode* right;
} treeNode;
treeNode* makeRootNode(char data, treeNode* leftNode, treeNode* rightNode) {
	treeNode* root = (treeNode*)malloc(sizeof(treeNode));
	root->data = data;
	root->left = leftNode;
	root->right = rightNode;
	return root;
}
void preorder(treeNode* root) {
	if (root) {
		printf("%c", root->data);
		preorder(root->left);
		preorder(root->right);
	}
}
void inorder(treeNode* root) {
	if (root) {
		inorder(root->left);
		printf("%c", root->data);
		inorder(root->right);
	}
}
void postorder(treeNode* root) {
	if (root) {
		postorder(root->left);
		postorder(root->right);
		printf("%c", root->data);
	}
}
void main() {
	treeNode* n7 = makeRootNode('D', NULL, NULL);
	treeNode* n6 = makeRootNode('C', NULL, NULL);
	treeNode* n5 = makeRootNode('B', NULL, NULL);
	treeNode* n4 = makeRootNode('A', NULL, NULL);
	treeNode* n3 = makeRootNode('/', n6, n7);
	treeNode* n2 = makeRootNode('*', n4, n5);
	treeNode* n1 = makeRootNode('-', n2, n3);
	printf("\n preorder : ");
	preorder(n1);
	printf("\n inorder : ");
	inorder(n1);
	printf("\n postorder : ");
	postorder(n1);
	getchar();
}
```

***

### 그래프

![](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQ1t-ky1GOITfzgeO9F9UvehxXFxXMvTD8_kCkYSw3-mfsUzV7C)

그래프의 구성 요소에는 특정 위치를 나타내는 노드, 노드 간의 관계를 나타내는 간선이 있고 모든 그래프는 정점과 간선의 집합으로 이루어진다고 할 수 있으며 사이클을 가질 수 있다. 사이클은 트리와 그래프를 구분하는 가장 큰 차이점이다.

### 그래프의 종류

Directed Graph - 방향이 있는 그래프

Undirected Graph - 방향이 없는 그래프

Cyclic Graph - 최소 하나의 원이 있는 그래프

Acyclic Graph - 원이 하나도 없는 그래프

### 예제 코드

```
#include <stdio.h>
#include <stdlib.h>
struct AdjListNode
{
	int dest;
	struct AdjListNode* next;
};
struct AdjList
{
	struct AdjListNode* head;
};
struct Graph
{
	int V;
	struct AdjList* array;
};
struct AdjListNode* newAdjListNode(int dest)
{
	struct AdjListNode* newNode =
		(struct AdjListNode*) malloc(sizeof(struct AdjListNode));
	newNode->dest = dest;
	newNode->next = NULL;
	return newNode;
}
struct Graph* createGraph(int V)
{
	struct Graph* graph =
		(struct Graph*) malloc(sizeof(struct Graph));
	graph->V = V;
	graph->array =
		(struct AdjList*) malloc(V * sizeof(struct AdjList));
	int i;
	for (i = 0; i < V; ++i)
		graph->array[i].head = NULL;
	return graph;
}
void addEdge(struct Graph* graph, int src, int dest)
{
	struct AdjListNode* newNode = newAdjListNode(dest);
	newNode->next = graph->array[src].head;
	graph->array[src].head = newNode;
	newNode = newAdjListNode(src);
	newNode->next = graph->array[dest].head;
	graph->array[dest].head = newNode;
}
void printGraph(struct Graph* graph)
{
	int v;
	for (v = 0; v < graph->V; ++v)
	{
		struct AdjListNode* pCrawl = graph->array[v].head;
		printf("\n Adjacency list of vertex %d\n head ", v);
		while (pCrawl)
		{
			printf("-> %d", pCrawl->dest);
			pCrawl = pCrawl->next;
		}
		printf("\n");
	}
}
int main()
{
	int V = 5;
	struct Graph* graph = createGraph(V);
	addEdge(graph, 0, 1);
	addEdge(graph, 0, 4);
	addEdge(graph, 1, 2);
	addEdge(graph, 1, 3);
	addEdge(graph, 1, 4);
	addEdge(graph, 2, 3);
	addEdge(graph, 3, 4);
	printGraph(graph);
	return 0;
}

```

***

### 소감

리스트, 트리 그리고 그래프가 무엇인지 수업과 영상 그리고 검색 등을 통해서 학습하면서 이 자료구조들을 코드로 비록 저의 힘만으로 구현할 수는 없었지만 예제들을 찾아보고 이해하면서 제 것으로 만들 수 있었던 것 같습니다. 그리고 마크다운을 활용해서 깃허브를 다양하게 꾸밀 수 있다는 걸 배우고 나서 깃허브가 새롭게 보이는 것 같습니다. 과제를 하면서 이해하기 어렵고 힘든 부분이 많았지만 끝마치고 나서는 정말 뿌듯함을 느꼇고 부족한 부분은 더욱 열심히 공부를 해야겠다는 생각이 들었습니다!
