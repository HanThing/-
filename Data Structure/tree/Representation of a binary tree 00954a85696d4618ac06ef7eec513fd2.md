# Representation of a binary tree

# array로 표현

       a
      /   \
    b     c
   /  \   /   \
  d   e f   g

위의 binary tree의 각 노드를 배열에 저장한다면, a, b, c, d, e, f, g 순서대로 넣을 것이다. 배열이기 때문에, a는 인덱스 0이라고 하는게 맞지만, 편의상 1이라고 생각 하겠다. 그럼 아래와 같은 표로 인덱스간의 관계를 표현 해 볼 수 있다.

| 노드 | 인덱스 | 왼쪽 자식 | 오른쪽 자식 |
| --- | --- | --- | --- |
| a | 1 | 2 | 3 |
| b | 2 | 4 | 5 |
| c | 3 | 6 | 7 |
|  |  |  |  |

위 표를 통해 수식을 도출하면, 다음과 같다.

element: i

Lchild: i*2

Rchild: i*2+1

parent: i/2

# doubly linked list로 표현

       a
      /   \
    b     c
   /  \   /   \
  d   e f   g

이번엔 위의  binary tree를 doubly linked list로 표현할 것이다. 각각의 노드는 Lchild와 Rchild의 주소를 저장하는 포인터 2개와 데이터를 저장하는 변수 1개로 구성된다.

노드개수 n: 7

NULL개수: n+1

e(external node)=i(internal node)+1

# Full binary tree vs Complete binary tree

: full binary tree는 다음과 같다.

       a
      /   \
    b     c
   /  \   /   \
  d   e f   g

따라서 노드의 개수 n은 $2^{h+1}$ - 1 이다.

: complete binary tree는 다음과 같다.

       a
      /   \
    b     c
   /  \   /   
  d   e f   

위 tree의 노드를 배열에 저장한다고 생각해보면, 인덱스 사이에 빈공간이 없다. 하지만, 아래의 트리를 배열에 넣는 다면, 빈공간이 생기게 된다.

       a
      /   \
    b     c
   /          \
 d            g

a, b, c, d, 빈공간, 빈공간, g로 배열에 저장되어야 위에서 정리했던 관계식을 사용할 수 있다. 즉, d와 g사이에 빈공간이 있기 때문에 이 트리는 complete binary tree가 아니게 된다. full binary tree는 당연히 complete binary tree라고 볼 수 있다.

- full binary tree:
    - 모든 내부 노드가 정확히 두 개의 자식 노드를 가지고 있다.
    - 모든 리프 노드는 같은 깊이에 있다.
- complete binary tree:
    - 마지막 레벨을 제외한 모든 레벨이 완전히 채워져 있다.
    - 마지막 레벨의 노드는 가능한 왼쪽부터 채워진다.