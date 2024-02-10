---
title: 数据结构和算法-树
tags:
  - algorithm
categories:
  - Data-Structure
mathjax: true
---
# 6.2 树的定义
树：树 ( Tree ) 是 n ( $n \geq 0$ ) 个结点的有限集 。 n=0 时称为空树 . 在任意一棵非空树中: 
1. 有旦仅有一个特定的称为根 ( Root ) 的结点；
2. 当 n > 1 时 , 其余结点可分为 $m ( m > 0 )$ 个互不相交的有限集 $T_1$、$T_2$、 ...... 、 $T_n$, 其中每一个集合本身又是一棵树，并且称为根的子树 ( SubTree )，如圈 6-2-1 所示 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307071139548.png)

## 6.2.1 结点分类
结点拥有的子树数称为结点的度 ( Degree )。度为 0 的结点称为叶结点(Leaf)或终端结点；度不为 0 的结点称为非终端结点或分支结点 。 除根结点之外，分支结点也称为内部结点。树的度是树内各结点的度的最大值。 如图 6-2-4 所示,因为这棵树结点的度的最大值是结点 D 的度，为 3，所以树的度也为 3 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307071350531.png)

## 6.2.2 结点间关系
- 结点的子树的根称为该结点的孩子( Child )，相应地，该结点称为孩子的双亲( Parent) 。
- 同一个双亲的孩子之间互称兄弟( Sibling)。
- 结点的祖先是从根到该结点所经分支上的所有结点。所以对于 H 来说 D、B、A 都是它的祖先。
- 以某结点为根的子树中的任一结点都称为该结点的子孙。B 的子孙有 D、G、H、I，如图 6-2-5 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307071359879.png)

## 6.2.3 树的其他相关概念
- 结点的层次( Level)：从根开始定义起，根为第一层，根的孩子为第二层。
- 堂兄弟：其双亲在同一层的结点直为堂兄弟。显然图 6-2-6 中的 D、 E、 F 是堂兄弟,而 G 、 H、 l 、 J 也是。
- 树的深度( Depth )或高度：树中结点的最大层次称为树的深度( Depth )或高度，当前树的深度为 4。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307071408146.png)
- 如果将树中结点的各子树看成从左至右是有次序的 , 不能互换的,则称该树为有序树,否则称为无序树。
- 森林 ( Forest) 是 $m(m \geq 0 )$ 棵互不相交的树的集合 。对树中每个结点而言 ,其子树的集合即为森林。对于图 6-2-1 中的树而言,图 6- 2 - 2 中的两棵子树其实就可以理解为森林。![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307071139548.png)

# 6.3 树的抽象数据类型
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072013257.png)

# 6.4 树的存储结构

## 6.4.1 双亲表示法
我们假设以一组连续空间存储树的结点，同时在每个结点中，附设一个指示器指示其双亲结点到链表中的位置。也就是说,每个结点除了知道自己是谁以外,还知道它的双亲在哪里。它的结点结构为表 6-4-1 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072023825.png)
其中 data 是数据域，存储结点的数据信息。而 parent 是指针域,存储该结点的双亲在数组中的下标。

以下是我们的双亲表示法的结点结构定义代码。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072024492.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072025221.png)

由于根结点是没有双亲的，所以我们约定根结点的位置域设置为 -1.
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072029693.png)

结点的孩子是什么？
增加一个结点最左边孩子的域，命名为长子域,这样就可以很容易得到结点的孩子。如果没有孩子的结点,这个长子域就设置为 -1 ,如表 6-4-3 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072251552.png)

如何获取各兄弟之间的关系？
增加一个右兄弟域来体现兄弟关系,也就是说,每一个结点如果它存在右兄弟,则记录下右兄弟的下标。同样的,如果右兄弟不存在,则赋值为 -1 ,如表 6-4-4 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072254663.png)

## 6.4.2 孩子表示法
由于树中每个结点可能有多棵子树，可以考虑用多重链表，即每个结点有多个指针域，其中每个指针指向一棵子树的根结点，我们把这种方法叫做多重链表表示法。

### 方案一
一种是指针域的个数就等于树的度，树的度是树各个结点度的最大值，其结构如表 6-4-5 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072307115.png)

对于图 6-4-1 的树来说，树的度是 3，所以我们的指针域的个数是 3，这种方法实现如图 6-4-2 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072308588.png)

### 方案二
第二种方案每个结点指针域的个数等于该结点的度，我们专门取一个位置来存储结点指针域的个数，其结构如表 6-4-6 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072311295.png)

其中 data 为数据域，degree 为度域，也就是存储该结点的孩子结点的个数，child1 到 childd 为指针域，指向该结点的各个孩子的结点 。
对于图 6-4-2 的树来说，这种方法实现如图 6-4-3 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072312746.png)

缺点：在运算上会带来时间上的损耗 。
### 孩子表示法
把每个结点的孩子结点排列起来,以单链表作存储结构，则 n 个结点有 n 个孩子链表，如果是叶子结点则此单链表为空。然后 n 个头指针又组成一个线性表，采用顺序存储结构，存放进一个一维数组中 ,如图 6-4-4 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072325587.png)

为此，设计两种结点结构，一个是孩子链表的孩子结点，如表 6-4-7 所示。
其中 child 是数据域,用来存储某个结点在表头数组中的下标。 next 是指针域,用来存储指向某结点的下一个孩子结点的指针。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072331404.png)

另一个是表头数组的表头结点，如表 6-4-8 所示。
其中 data 是数据域，存储某结点的数据信息。firstchild 是头指针域，存储该结点的孩子链表的头指针。

以下是我们的孩子表示法的结构定义代码。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072339997.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072341748.png)

### 双亲孩子表示法
把双亲表示法和孩子表示法综合。解决孩子表示法不好访问父结点的问题。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307072343825.png)

## 6.4.3 孩子兄弟表示法
其中 data 是数据域，firstchild 为指针域，存储该结点的第一个孩子结点的存储地址，rightsib 是指针域，存储该结点的右兄弟结点的存储地址 。
结点结构如表 6-4-9 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080006110.png)
结构定义代码如下。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080008435.png)
对于图 6-4-1 的树来说,这种方法实现的示意图如图 6-4-6 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080009962.png)
这个表示法的最大好处是它把一棵复杂的树变成了一棵二叉树。我们把图6-4-6 变变形就成了图 6-4-7 这个样子。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080010770.png)
# 6.5 二叉树的定义
二叉树( Binary Tree )是 $n ( n \geq 0 )$个结点的有限集合，该集合或者为空集(称为空二叉树)，或者由一个根结点和两棵互不相交的、 分别称为根结点的左子树和右子树的二叉树组成 。
## 6.5.1 二叉树特点
二叉树的特点有：
- 每个结点最多有两棵子树，所以二叉树中不存在度大于 2 的结点。注意不是只有两棵子树，而是最多有，没有子树或者有一棵子树都是可以的。
- 左子树和右子树是有顺序的，次序不能任意颠倒。
- 即使树中某结点只有一棵子树，也要区分它是左子树还是右子树。
二叉树具有五种基本形态：
1. 空二叉树。
2. 只有一个根结点。
3. 根结点只有左子树。
4. 根结点只有右子树。
5. 根结点既有左子树又有右子树。
如果是有三个结点的树，有几种形态？如果是有三个结点的二叉树，有几种形态?
## 6.5.2 特殊二叉树
1. 斜树
    - 左斜树：所有的结点都只有左子树的二叉树；
    - 右斜树：所有结点都是只有右子树的二叉树；
    - 特点：每一层都只有一个结点,结点的个数与二叉树的深度相同；
    - 线性表结构可以理解为是树的一种极其特殊的表现形式 。
2. 满二叉树
    - 在一棵二叉树中，如果所有分支结点都存在左子树和右子树，并且所有叶子都在同一层上，这样的二叉树称为满二叉树；
    - 图 6-5-5 就是一棵满二叉树；![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080040503.png)
3. 完全二叉树
    - 对一棵具有 n 个结点的二叉树按层序编号,如果编号为 $i ( 1 \leq i \leq n )$ 的结点与同样深度的满二叉树中编号为 i 的结点在二叉树中位置完全相同,则这棵二叉树称为完全二叉树；
    - 如图 6-5-6 所示![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080043415.png)
# 6.6 二叉树的性质
1. 在二叉树的第 i 层上至多有 $2^{i-1}$ 个结点 $( i \geq 1 )$；
2. 深度为 k 的二叉树至多有 $2^k-1$ 个结点 $( k \geq 1 )$；
3. 对任何一棵二叉树 T，如果其终端结点数为 $n_0$， 度为 2 的结点数为 $n_2$，则 $n_0=n_2+1$
    - 树 T 结点总数 $n=n_0+n_1+n_2$
4. 具有 n 个结点的完全二叉树的深度为 $\lfloor \log_2n \rfloor+1$ ( $\lfloor x \rfloor$ 表示不大于 $x$ 的最大整数)；
5. 如果对一棵有 $n$ 个结点的完全二叉树(其深度为 $\lfloor \log_2n \rfloor+1$ )的结点按层序编号(从第 1 层到第 $\lfloor \log_2n \rfloor+1$ 层,每层从左到右),对任一结点 $i ( \leq i\leq n )$有：![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080109395.png)
# 6.7 二叉树的存储结构
## 6.7.1 二叉树顺序存储结构
顺序存储对树这种一对多的关系结构实现起来是比较困难的 。但是二叉树是一种特殊的树, 由于它的特殊性,使得用顺
序存储结构也可以实现。
完全二叉树的顺序存储,一棵完全二叉树如图 6-7-1 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080123831.png)
将这棵二叉树存入到数组中,相应的下标对应其同样的位置 , 如图 6-7-2 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080123149.png)
对于一般的二叉树,尽管层序编号不能反映逻辑关系,但是可以将其按完全二叉树编号,只不过,把不存在的结点设置为∧而已。如图 6-7-3 ,注意浅色结点表示不存在 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080128363.png)
## 6.7.2 二叉链表
data 是数据域, lchild 和 rchild 都是指针域,分别存放指向左孩子和右孩子的指针
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080130692.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080132117.png)
# 6.8 遍历二叉树
## 6.8.2 二叉树遍历方法
1. 前序遍历：根左右![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080137932.png)
2. 中序遍历：左根右![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080138069.png)
3. 后序遍历：左右根![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080140138.png)
4. 层序遍历：规则是若树为空,则空操作返回,否则从树的第一层,也就是根结点开始访问,从上而下逐层遍历,在同一层中,按从左到右的顺序对结点逐个访问 。如图 6-8-5 所示,遍历的顺序为: ABCDEFGHI![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080142811.png)
## 6.8.3 前序遍历算法
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080212381.png)
## 6.8.4 中序遍历算法
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080212775.png)
## 6.8.5 后序遍历算法
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307080213810.png)
## 6.8.6 推导遍历结果
- 己知前序遍历序列和中序遍历序列，可以唯一确定一棵二叉树。
- 已知后序遍历序列和中序遍历序列，可以唯一确定一棵二叉树 。
- 已知前序和后序遍历，是不能确定一棵二叉树的。
# 6.9 二叉树的建立
1. 二阶指针
2. 返回值
# 6.10 线索二叉树
## 6.10.1 线索二叉树原理
- 节约二叉链表的空间。一个有 n 个结点的二叉链表，有 n+1 个空指针域。
- 记住结点前驱和后继
我们把这种指向前驱和后继的指针称为线索，加上线索的二叉链表称为线索链表，相应的二叉树就称为线索二叉树(Threaded Binary Tree) 。
对二叉树以某种次序遍历使其变为线索二叉树的过程称做是线索化。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307081627935.png)
其中 :
- ltag 为 0 时指向该结点的左孩子,为 1 时指向该结点的前驱。
- rtag 为 0 时指向该结点的右孩子,为 1 时指向该结点的后继 .
- 因此对于图 6-10-1 的二叉链表图可以修改为图 6-10-5 的样子。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307081629286.png)
## 6.10.2 线索二叉树结构实现
线索化的实质就是将二叉链表中的空指针改为指向前驱或后继的线索。
和双向链表结构一样,在二叉树线索链表上添加一个头结点,如图 6-10-6 所示；
如果所用的二叉树需经常遍历或查找结点时需要某种遍历序列中的前驱和后继,那么采用线索二叉链表的存储结构就是非常不错的选择 。
# 6.11 树、森林与二叉树的转换
## 6.11.1 树转换为二叉树
将树转换为二叉树的步骤如下：
1. 加线。在所有兄弟结点之间加一条连线。
2. 去线。对树中每个结点，只保留它与第一个孩子结点的连线，删除它与其他孩子结点之间的连线。
3. 层次调整。以树的根结点为轴心,将整棵树顺时针旋转一定的角度,使之结构层次分明。注意第一个孩子是二叉树结点的左孩子,兄弟转换过来的孩子是结点的右孩子。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307082315500.png)
## 6.11.2 森林转换为二叉树
森林中的每一棵树都是兄弟，可以按照兄弟的处理办法来操作 。
1. 把每个树转换为二叉树。
2. 第一棵二叉树不动,从第二棵二叉树开始,依次把后一棵二叉树的根结点作为前一棵二叉树的根结点的右孩子,用线连接起来。当所有的二叉树连接起来后就得到了由森林转换来的二叉树。
例如图 6- 11-3 ,将森林的三棵树转化为一棵二叉树。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307082325009.png)
## 6.11.3 二叉树转换为树
二叉树转换为树是树转换为二叉树的逆过程,也就是反过来做而已。如图 6-11 -4所示。步骤如下：
1. 加线。若某结点的左孩子结点存在,则将这个左孩子的右孩子结点、右孩子的右孩子结点、右孩子的右孩子的右孩子结点......哈,反正就是左孩子的 n 个右孩子结点都作为此结点的孩子。 将该结点与这些右孩子结点用线连接起来。
2. 去线。删除原二叉树中所有结点与其右孩子结点的连线。
3. 层次调整。使之结构层次分明。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090210189.png)
## 6.11.4 二叉树转换为森林
判断一棵二叉树能够转换成一棵树还是森林，标准很简单，那就是只要看这棵二叉树的根结点有没有右孩子，有就是森林，没有就是一棵树。那么如果是转换成森林，步骤如下：
1. 从根结点开始，若右孩子存在，则把与右孩子结点的连线删除，再查看分离后的二叉树，若右孩子存在，则连线删除......，直到所有右孩子连线都删除为止，得到分离的二叉树。
2. 再将每棵分离后的二叉树转换为树即可。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090230825.png)
## 6.11.5 树与森林的遍历
树的遍历分为两种方式。
1. 一种是先根遍历树,即先访问树的根结点,然后依次先根遍历根的每棵子树。
2. 另一种是后根遍历，即先依次后根遍历每棵子树，然后再访问根结点。比如图6-11-4 中最右侧的树，它的先根遍历序列为 ABEFCDG，后根遍历序列为EFBCGDA.

森林的遍历也分为两种方式：
1. 前序遍历: 先访问森林中第一棵树的根结点，然后再依次先根遍历根的每棵子树，再依放用同样方式遍历除去第一棵树的剩余树构成的森林。比如图 6-11-5右侧三棵树的森林,前序遍历序列的结果就是 ABCDEFGHJI。
2. 后序遍历: 是先访问森林中第一棵树,后根遍历的方式遍历每棵子树,然后再访问根结点 ,再依次同样方式遍历除去第一棵树的剩余树构成的森林。比如图6- 11-5 右侧三棵树的森林,后序遍历序列的结果就是 BCDAFEJHIG。
# 6.12 赫夫曼树及其应用
## 6.12.1 赫夫曼树
最基本的压缩编码方法一一赫夫曼编码
if else 是树状结构
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090255393.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090256153.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090256872.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090256091.png)
## 6.12.2 赫夫曼树定义与原理
- Weighted Path Length of Tree
- 从树中一个结点到另一个结点之间的分支构成两个结点之间的路径，路径上的分支数目称做路径长度； 树的路径长度就是从树根到每一结点的路径长度之和。
- 结点的带权的路径长度为从该结点到树根之间的路径长度与结点上权的乘积；树的带权路径长度为树中所有叶子结点的带权路径长度之和。
- WPL 最小的二叉树称做赫夫曼树。

构造方法：
## 6.12.3 赫夫曼编码
