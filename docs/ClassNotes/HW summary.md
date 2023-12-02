HW summary

#### HW2

**1-1**![image-20231104084918878](HW%20summary/image-20231104084918878.png)

**1-2**If a linear list is represented by a linked list, the addresses of the elements in the memory must be consecutive.(F)

**2-1**

![image-20231104084946221](HW%20summary/image-20231104084946221.png)

**2-2**

![image-20231104084956995](HW%20summary/image-20231104084956995.png)

**2-3**![image-20231104085009356](HW%20summary/image-20231104085009356.png)

```c
// Add Two Polynomials
Polynomial Add(Polynomial a, Polynomial b){
    Polynomial sum, pa, pb, psum, sumnow;
    sum = (Polynomial)malloc(sizeof(struct Node));
    sumnow = sum;
    pa = a;
    pb = b;
    int exa, exb, find_flag = 0;
    while(1){
        psum = (Polynomial)malloc(sizeof(struct Node));
        exa = pa->Exponent;
        exb = pb->Exponent;
        psum->Next = NULL;
        psum->Exponent = exa >= exb ? exa : exb;
        psum->Coefficient = exa > exb ? pa->Coefficient : pb->Coefficient;
        if (exa == exb){
            psum->Coefficient = pa->Coefficient + pb->Coefficient;
            //printf("%d + %d\n",pa->Coefficient,pb->Coefficient);
        }
        if (psum->Coefficient != 0 ){
            sumnow->Next = psum;
            sumnow = psum;
            //printf("add p %d %d\n",psum->Coefficient, psum->Exponent);
        }
        if (exa == exb){
            if(pa->Next == NULL || pb->Next == NULL){
            //printf("before break %d %d \n", pa->Exponent, pb->Exponent);
            break;
        }  
                pa = pa->Next;
                pb = pb->Next;
        } else if (exa > exb && pa->Next != NULL){
            pa = pa->Next;
        } else if (pb->Next != NULL){
            pb = pb->Next;
        }
    }
    if (pa->Next != NULL){
        sumnow->Next = pa->Next;
    }
    if (pb->Next != NULL){
        sumnow->Next = pb->Next;
    }
    return sum;
}
```

```c
// Reverse Linked List
List Reverse( List L ){
    List cur, head, prev;
    head = NULL;
    cur = L->Next;
    prev = L->Next;
    while(cur->Next){
       	prev = cur;
     	cur = cur->Next;
        prev->Next = head;
        head = prev;
    }
    cur->Next = prev;
    L->Next = cur;
    return L
}

List Reverse(List L){
    List new_head, old_head, tmp;
    new_head = NULL; 
    tmp = L->Next;
    while(tmp){
        old_head = tmp;
        tmp = tmp->Next;
        old_head -> Next = new_head;
        new_head = old_head;
    }
    L->Next = new_head;
    return L;
}
```

#### HW3

**2-1**![image-20231104084444442](HW%20summary/image-20231104084444442.png)

> 1. push(o o o) pop(o o o) push(p) pop(p) push(s) pop(s)
> 2. push(o o) pop (o o) push(o) pop(o)
> 3. push(o) pop(o) push(o o) pop(o o)
> 4. push(o) pop(o) push(o) pop(o) push(o) pop(o)
> 5. push(o o) pop(o) push(o) pop(o o)

**2-2**![image-20231104084756281](HW%20summary/image-20231104084756281.png)

```c
// Pop Sequence
#include <stdio.h>

void Push(int *st, int value);
int Pop(int *st);

int main() {
    int M, N, K, flag=1;
    scanf("%d %d %d", &M, &N, &K);
    for(int iter=0;iter<K;iter++) {
        int st[M + 1], a[N], input[N];
        st[0] = 0;
        flag = 1;
        int *ptr = a;
        for (int i = 0; i < N; i++) {
            scanf("%d", &input[i]);
            a[i] = i + 1;
        }
        for (int i = 0; i < N; i++) {
            while (st[0] == 0 || input[i] > st[*st]) {
                Push(st, *ptr);
                ptr++;
                if (st[0] > M || ptr > &a[N]) {
                    printf("NO\n");
                    flag=0;
                    break;
                }
            }
            if (input[i] == st[*st]) {
                Pop(st);
            }
            if (input[i] < st[*st]) {
                printf("NO\n");
                flag=0;
                break;
            }
            if(flag == 0){
                break;
            }
        }
        if(st[0] == 0 && flag){
            printf("YES\n");
        }
        
    }
    return 0;
}

void Push(int *st, int value){
    st[++*st] = value;
}
int Pop(int *st){
    int value = st[*st];
    (*st)--;
    return value;
}
```



**2-3**![image-20231104084818500](HW%20summary/image-20231104084818500.png)

#### HW4

**1-1**:It is always possible to represent a tree by a one-dimensional integer array.(T)

> n叉树，对于每个父节点i，他的子节点可以存放在 ni, ni+1, ni+2...

**1-2**:There exists a binary tree with 2016 nodes in total, and with 16 nodes having only one child.(F)

> 假设没有孩子的结点（叶结点）个数为n₀，只有一个孩子的结点（度为1的结点）个数为n₁，有两个孩子的结点（度为2的结点）个数为n₂。
> 则n₀+n₁+n₂=2016 ∵n₀=n₂+1（二叉树的性质：叶结点个数等于度为2的结点个数加1） ∴n₀+n₁+n₂=2016
> ⇨n₂+1+16+n₂=2016 ⇨2n₂=1999 n₂除不尽，所以答案错误。

**2-1**

![image-20231104084014189](HW%20summary/image-20231104084014189.png)

**2-2**![image-20231104084032340](HW%20summary/image-20231104084032340.png)

**2-3**![image-20231104084146353](HW%20summary/image-20231104084146353.png)

**2-4**

![image-20231104084218617](HW%20summary/image-20231104084218617.png)

> 左边空，指向遍历顺序的前一个节点。右边空，指向遍历顺序的后一个节点

```c
//树同构的判断
int Isomorphic(Tree T1, Tree T2){
    Tree ptrt1 = T1, ptrt2 = T2;
    int flag1 = 0, flag2 = 0, result = 1;
    if(ptrt1 == NULL && ptrt2 == NULL){
        return 1;
    } else if (ptrt1 == NULL || ptrt2 == NULL){
        return 0;
    }
    if(ptrt1->Element == ptrt2->Element){
        flag1 = Isomorphic(ptrt1->Left, ptrt2->Left);
        if(flag1){
            flag2 = Isomorphic(ptrt1->Right, ptrt2->Right);
        } else {
            flag1 = Isomorphic(ptrt1->Left, ptrt2->Right);
            flag2 = Isomorphic(ptrt1->Right, ptrt2->Left);
        }
        result = result & flag1 & flag2;
    } else {
        return 0;
    }
    if(result){
        return 1;
    } else {
        return 0;
    }
}
```

```c
// zigzagging
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode *Tree;
struct TreeNode{
    int value;
    Tree Left;
    Tree Right;
};

Tree inductFromTwoOrders(int *io, int *po, int size);
int findI(int i, int *A, int size);
void levelOrder(Tree ptr);
int main(){
    int N, inorder[30], postorder[30];
    scanf("%d",&N);
    for(int i=0; i<N; i++){
        scanf("%d", &inorder[i]);
    }
    for(int i=0; i<N; i++){
        scanf("%d", &postorder[i]);
    }
    Tree p = inductFromTwoOrders(inorder, postorder, N);
    
    //printf("%d %d %d", p->value, p->Left->value, p->Right->value);
    levelOrder(p);
}

void levelOrder(Tree ptr){
    int first = 1;
    Tree q;
    int level[35] = {0}, current_level = 0;
    int stack[35] = {0};
    level[0] = 1;
    struct TreeNode qu[100];
    int r = 0, l = 0;
    qu[++r] = *ptr;
    while(r-l!=0){
        q = &qu[++l];
        if(current_level%2 == 1){
            printf(" %d",q->value);
        } else if(current_level == 0){
            printf("%d",q->value);
        } else{
            stack[++stack[0]]=q->value;
        }
        if(q->Left!=NULL){
            qu[++r] = *(q->Left);
            level[current_level+1]++;
        }
        if(q->Right!=NULL){
            qu[++r] = *(q->Right);
            level[current_level+1]++;
        }
        level[current_level]--;
        if(level[current_level]== 0){
            current_level++;
            while(stack[0]>0){
                printf(" %d",stack[stack[0]]);
                stack[0]--;
            }
        }
    }
    
}
Tree inductFromTwoOrders(int *io, int *po, int size){
    int cut_pos = findI(po[size-1], io, size);
    if(cut_pos == -1){
        printf("error\n");
        return 0;
    }
    Tree root = (Tree)malloc(sizeof(struct TreeNode));
    root->value = po[size-1];
    //printf("value :%d\n", root->value);
    int *left = io, l_size = cut_pos;
    int *right = io + cut_pos+1, r_size = size - cut_pos - 1;
    int *po_left = po, *po_right = &po[cut_pos];
    if (l_size == 0){
        root->Left = NULL;
    } else {
        root->Left = inductFromTwoOrders(left, po_left, l_size);
    }
    if (r_size == 0){
        root->Right = NULL;
    } else {
        root->Right = inductFromTwoOrders(right, po_right, r_size);
    }    
    return root;
    
}

int findI(int i, int *A, int size){
    if(i == 5){
        int p = 0;
    }
    for(int j=0; j<size; j++){
        if(A[j] == i){
            return j;
        }
    }
    return -1;
}
```



#### HW5

**1-1**:In a binary search tree, the keys on the same level from left to right must be in sorted (non-decreasing) order.

**1-2**:In a binary search tree which contains several integer keys including 4, 5, and 6, if 4 and 6 are on the same level, then 5 must be their parent.（F）

> 5可以作为4和6的祖先，不一定作为直接连接的父母。比如可以是4 <- 2 <- 5 -> 7 -> 6，此时4和6依然在一个层次上。

![image-20231024231738732](HW%20summary/image-20231024231738732.png)

![image-20231024231758743](HW%20summary/image-20231024231758743.png)

![image-20231024093118100](HW%20summary/image-20231024093118100.png)

![image-20231024231827584](HW%20summary/image-20231024231827584.png)

![image-20231024231845817](HW%20summary/image-20231024231845817.png)

https://blog.csdn.net/best_LY/article/details/120956505

[折半查找的判定树](https://blog.csdn.net/qq_59183443/article/details/128199099)

https://blog.csdn.net/weixin_53965540/article/details/121583290

https://blog.51cto.com/u_14866376/4858577

> 若选择向上取整：对于该树中每个结点的左子树都大于等于右子树高度，且每个结点的左子树上的结点个数都大于等于右子树上的结点个数。
>
> 若选择向下取整：对于该树中每个结点的左子树都小于等于右子树高度，且每个结点的左子树上的结点个数都小于等于右子树上的结点个数。

```
List Reverse(List L){
    List ptr1 = L->Next, prev = NULL, cur = L->Next;
    while (ptr1 != NULL){
        ptr1 = ptr1->Next;
        cur->Next = prev;
        prev = cur;
        cur = ptr1;
    }
    L->Next = prev;
    return L;
```

#### HW6

1-1: If a complete binary tree with 137 nodes is stored in an array (root at position 1), then the nodes at positions 128 and 137 are at the same level. ==T==

> 相同深度h的节点在2^h ~ 2^(h+1)-1范围内。注意根的深度为0

1-2: The inorder traversal sequence of any min-heap must be in sorted order. ==F==

> 4 <- 1 -> 5 inorder traversal is 4 1 5

![image-20231107143323519](HW%20summary/image-20231107143323519.png)

![image-20231107143336858](HW%20summary/image-20231107143336858.png)

![image-20231107143346674](HW%20summary/image-20231107143346674.png)



![image-20231107143357121](HW%20summary/image-20231107143357121.png)

![image-20231107143413984](HW%20summary/image-20231107143413984.png)

![image-20231107143424693](HW%20summary/image-20231107143424693.png)

> 也可能是倒数第二层，比如说最后新加入了一个小于最大值（最左叶子）的节点，这个节点会作为最大节点的左孩子，那么最大节点就不是叶子结点了，但它仍然是最大的节点。

```c
/* 编程题 完全二叉搜索树*/
#include <stdio.h>
int input[1010], output[1010], n, t = 0;

void sort(int *A, int N){
    for(int i=0; i<N; i++){
        for(int j=0; j<N-i-1; j++){
            if(A[j] > A[j+1]){
                int temp = A[j];
                A[j] = A[j+1];
                A[j+1] = temp;
            }
        }
    }
}

void inOrder(int root) {
    if (root >= n) return ;
    inOrder(root * 2 + 1);
    level[root] = in[t++];
    inOrder(root * 2 + 2);
}

int main() {
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
        scanf("%d", &input[i]);
    sort(input, n);
    inOrder(0);
    printf("%d", output[0]);
    for (int i = 1; i < n; i++)
        printf(" %d", output[i]);
    return 0;
}

```

```c
/* 6-1 Percolate Up and Down */

void PercolateUp( int p, PriorityQueue H ){
    ElementType x = H->Elements[p];
    int i;
    for(i=p; H->Elements[i/2] > x; i = i/2){
        H->Elements[i] = H->Elements[i/2];
    }
    H->Elements[i] = x;
}
void PercolateDown( int p, PriorityQueue H ){
    ElementType x = H->Elements[p];
    int i;
    int Child;
    for(i = p; 2*i <= H->Size; i = Child){
        Child = 2*i;
        if(Child+1 <= H->Size && H->Elements[Child+1] < H->Elements[Child]){
            Child += 1;
        }
        if(x > H->Elements[Child]){
            H->Elements[i] = H->Elements[Child];
        } else {
            break;
        }
    }
    H->Elements[i] = x;
}

```

#### HW7

1-1: In Union/Find algorithm, if Unions are done by size, the depth of any node must be no more than N/2, but not O(logN). ==F==

> Time complexity of N Union and M Find operations is now O( N + M log2 N ).
> Let T be a tree created by union-by-size with N nodes, then height(T)<=(log2N)+1;

2-1: ![image-20231107142425296](HW%20summary/image-20231107142425296.png)

![image-20231107142439770](HW%20summary/image-20231107142439770.png)

![image-20231107142452898](HW%20summary/image-20231107142452898.png)

#### HW8

1-1: In a connected graph, the number of edges must be greater than the number of vertices minus 1. ==F==

> equal or greater than (no less than)

1-2: In a directed graph, the sum of the in-degrees must be equal to the sum of the out-degrees of all the vertices. ==T==

1-3: If a directed graph G=(V, E) is weakly connected, then there must be at least |V| edges in G. ==F==

> at least |V|-1 edges

2-1: If graph G is NOT connected and has 35 edges, then it must have at least ____ vertices.

> ==10==
>
> $\frac{(n-1)(n-2)}2 \geq 35$即除了一个孤立节点意外的子图，至少涵盖所有的边

2-2: A graph with 90 vertices and 20 edges must have at least __ connected component(s).

> ==70==
>
> 对于多个联通分量的图 r = E - V + C + 1
>
> 1 = 20 - 90 + C + 1

![image-20231114162913478](HW%20summary/image-20231114162913478.png)

2-4: Given an undirected graph G with 16 edges, where 3 vertices are of degree 4, 4 vertices are of degree 3, and all the other vertices are of degrees less than 3. Then G must have at least __ vertices.

> ==11==
>
> 32 = 12 + 12 + 2 * n
>
> n = 4
>
> V = 3 + 4 + 4

![image-20231114163103130](HW%20summary/image-20231114163103130.png)

```c
//6-1 Is Topological Orger

void updateDeg(int *deg, LGraph Graph){
    for(int i=0; i<=Graph->Nv;i++){
        deg[i] = 0;
    }
    for(int i=0; i<Graph->Nv; i++){
        PtrToAdjVNode pNode = Graph->G[i].FirstEdge;
        while(pNode!= NULL){
            deg[pNode->AdjV]++;
            pNode = pNode->Next;
        }
    }
}

bool IsTopSeq( LGraph Graph, Vertex Seq[] ){
    int deg[MaxVertexNum];
    updateDeg(deg, Graph);
    for(int i=0; i<Graph->Nv; i++){
        if(deg[Seq[i]-1] == 0){
            //printf("remove %d\n",Seq[i]-1);
            PtrToAdjVNode pNode = Graph->G[Seq[i]-1].FirstEdge;
            while(pNode!= NULL){
                deg[pNode->AdjV]--;
                pNode = pNode->Next;
            }
        } else {
            return false;
        }
    }
    return true;
}

```

```c
//7-1 Hamiltonian Cycle
#include <stdio.h>

int G[201][201] = {0};
int V, E;
int Hamilton(int Seq[], int len){
    if(Seq[0] != Seq[len-1] || len != V+1){
        return 0;
    }
    int mark[V+1];
    for(int i=1; i<=V; i++){
        mark[i] = 0;
    }
    for(int i=0; i<len-1; i++) {
        int v_s = Seq[i], v_e = Seq[i + 1];
        mark[v_e] = mark[v_s] = 1;
        if(G[v_s][v_e] == 0){
            return 0;
        }
    }

    for(int i=1; i<=V; i++){
        if(mark[i] == 0){
            return 0;
        }
    }
    return 1;
}
int main(){
    scanf("%d %d",&V, &E);
    for(int i=0; i<E; i++){
        int v_s,v_e;
        scanf("%d %d", &v_s, &v_e);
        G[v_s][v_e] = G[v_e][v_s] = 1;
    }
    int N;
    scanf("%d",&N);
    for(int i=0; i<N; i++){
        int len;
        scanf("%d",&len);
        int Seq[len];
        for(int j=0; j<len; j++){
            scanf("%d",&Seq[j]);
        }
        if(Hamilton(Seq,len)){
            printf("YES\n");
        } else {
            printf("NO\n");
        }
    }
}
```

#### HW9

1-1:In a weighted undirected graph, if the length of the shortest path from `b` to `a` is 12, and there exists an edge of weight 2 between `c` and `b`, then the length of the shortest path from `c` to `a` must be no less than 10. ==T==

> 如果c在b-a的最短路上，那么c-a的最短路就为10
>
> 如果c不在最短路上，那么c-a的最短路就不确定，但是必须要大于10，不然c-a的距离就小于等于9，那么b-a的最短路就可以更新为c-b-a = c-a + b-a <= 9 + 2 = 11

#### HW10

2-1

<img src="HW%20summary/image-20231129091204303.png" alt="image-20231129091204303" style="zoom:50%;" />

2-2

<img src="HW%20summary/image-20231129091214905.png" alt="image-20231129091214905" style="zoom:50%;" />

> 当且仅当G联通时最小生成树存在。（但不保证unique）

2-3

![image-20231129091308325](HW%20summary/image-20231129091308325.png)

2-4

![image-20231129091323133](HW%20summary/image-20231129091323133.png)
