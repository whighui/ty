# ==算法总结==

>1. `Character:toLowerCase()   toUpperCase() ` 数字或非字符不受影响
>2. `cahr c ^ ' '` 这种形式转换成数字 在 转换成字符 就完成小写-->大写  大写--->小写
>3. 返回类型若是二维数组  `List<int[]> list = new ArrayList<>();`  `return list.toArray(new int[list.size()][]);` 因为`Int[]`是引用类型
>4. 如是一维数组可以迭代进行转换 或者就是 `java` 流表达式 `return list.stream().mapToInt(Integer::intValue).toArray();`
>5. `Math.pow 和 Math.sqrt 传入参数是double` 返回类型是`double`   而`math.max math.min math.abs`这三个是根据传进来得参数来具体来返回值呗
>6. 基本类型变量方法传递得时候传递得是值， 引用类型变量方法传递是传递得引用 
>7. 斐波那契递归： 是一个二叉树的形式 时间复杂度 2^n 空间复杂度O(n)   但是用动态规划做就是降低了时间复杂度O(n) 空间复杂度O(1)
>8. 什么时候不用空间降低时间复杂度： 采用临时变量 不采用数据结构  例如滑动窗口 采用临时变量 不使用HashMap<>();
>
>9. 什么算法降低时间复杂度最快：动态规划
>
>10. 深搜的思想是栈  而广搜的思想就是队列
>
>11. 队列的底层是什么  可以怎么实现 链表、数组可以分别实现   还有c++Deque双端队列 数组+链表+中心控制器的实现方式
>12. https://cloud.tencent.com/developer/user/1121068   不错的博客
>

**动态规划和贪心算法区别**

>**动态规划算法和贪心算法有一个显著区别：**
>
>1. 在动态规划算法中，以自底向上的方式来利用最优子结构，也就是说，首先找到子问题的最优解，解决子问题，然后找到问题的一个最优解。
>2. 在贪心算法中，以自顶向下的方式使用最优子结构，也就是说，贪心算法会先做出选择，在当时看起来是最优的选择，然后再求解一个结果子问题，而不是先求解子问题的最优解，然后再做出选择。
>
>两者的不同点：
>1 贪心算法作出的每步贪心决策都无法改变，因为贪心策略是由上一步的最优解推导下一步的最优解，而上一部之前的最优解则不作保留。
>
>2 动态规划算法的全局最优解中一定包含某个局部最优解，但不一定包含前一个局部最优解，因此需要记录之前的所有局部最优解；保存局部最优解

# ==------------------------------------------------------------回溯 +Dfs==

>```xml
>result = []
>def backtrack(路径, 选择列表):
>if 满足结束条件:
>   result.add(路径)
>   return
>
>for 选择 in 选择列表:
>   做选择
>   backtrack(路径, 选择列表)
>   撤销选择
>```
>
>- **对于题目中的做法   回溯一般有两种情况：  一种是组合 一种是排列    两种方法使用的技巧也不相同**:
>
>```xml
>public void backtrack(LinkedList<>() list, boolean[] visited) ; 
>public void backtrack(LinkedList<>() list, int begin) 			 
>
>什么时候使用 visited 数组，什么时候使用 begin 变量
>
>排列问题，  讲究顺序（即 [2, 2, 3] 与 [2, 3, 2] 视为不同列表时），    用 visited 数组；
>组合问题，不讲究顺序（即 [2, 2, 3] 与 [2, 3, 2] 视为相同列表时），     用 begin 变量。
>
>剪枝条件：
>排列问题：visited[]数组  重复元素`if(i>0 && nums[i]==nums[i-1] && visited[i-1]==false)` 进行剪枝
>```
>
>同时
>
>-------
>
>**回溯跟递归区别：**
>
>1. 为了描述问题的某一状态，必须用到该状态的上一状态，而描述上一状态，又必须用到上一状态的上一状态……这种用自已来定义自己的方法，称为递归定义。
>2. 从问题的某一种可能出发, 搜索从这种情况出发所能达到的所有可能, 当这一条路走到” 尽头 “的时候, 再倒回出发点, 从另一个可能出发, 继续搜索. 这种不断” 回溯 “寻找解的方法, 称作” 回溯法 “。
>3. 递归是一种算法结构，递归会出现在子程序中自己调用自己或间接地自己调用自己。回溯有“剪枝”功能，





## [全排列](https://leetcode-cn.com/problems/permutations/)

>```
>输入：nums = [1,2,3]
>输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
>```
>
>1. 回溯+剪枝（`boolean[] visited`数组判断是否拜访过）
>
>----
>
>1. 时间复杂度：*O*(*n*×*n*!)，其中 *n* 为序列的长度  O(n)是添加答案需要遍历数组  O(n!)需要遍历这些次  寻找答案
>2. 空间复杂度：标记是否拜访过 O(N)      同时在递归的时候栈深度会达到 O(n)，因此总空间复杂度为 O(n + n)=O(2n)
>
>-------
>
>进阶：
>
>字节电商直播一面 问我可以可以不使用递归 也就是O(1)的空间复杂度完成
>
>[下一个排列](https://leetcode-cn.com/problems/next-permutation/)  就是使用规律来完成 找当前排列的下一个排列 重点
>
>----------
>
>在这里需要空间复杂度为O(1) 采用下一个排列知识点  在这里就是进行简单修改一下返回值再做 要不然就是太麻烦了
>
>```java
>    public List<int[]> permute(int[] nums) {
>        if (nums == null || nums.length == 0) return null;
>        List<int[]> ret = new ArrayList<>();
>        int count = 1, len = nums.length;
>        while (len > 0) {
>            count *= len;
>            len--;
>        }
>        Arrays.sort(nums);
>        for (int i = 0; i < count; i++) {
>            int[] temp = new int[nums.length];   //就是一定要记住数组是引用类型 这里边就是一定要new才是可以的
>            //因为Java里边在这里就是引用传递 所以在这里就是必须要小心 重新再创建一个数组呗
>            nums = nextPermutation(nums);  //这里边就是可以说 temp本身就是Nums么 就是因为在这里实现的么
>            for (int j = 0; j < nums.length; j++) {
>                temp[j] = nums[j];   
>            }
>            ret.add(temp);
>        }
>        return ret;
>    }
>
>
>    //在这里边我们是原地改变的nums呗 所以在nums传进来 原来的Nums也是做了改变
>    public int[] nextPermutation(int[] nums) {
>        int len = nums.length, l = len - 1;
>        int left = 0, right = len - 1;
>        for (int i = len - 1; i >= 1; i--) {
>            //第一步找到不满足符合条件的第一个数字  就是不满足降序排列
>            if (nums[i] <= nums[i - 1]) continue;
>            else {
>                //找到一个就是不满足的  nums[i-1]<nums[i] 之后我们就是找到比nums[i-1]大的一个数字
>                while (nums[l] <= nums[i - 1]) {
>                    l--;    //重后边遍历 找到第一个比他大的数字在这里就是可以呢呗 因为重后边往前边是升序排列
>                }
>                swap(nums, i - 1, l);
>                left = i;
>                break;
>            }
>        }
>        //例如 【0,5,4,3,2,1】-->[1,5,4,3,2,0]--->[1,0,2,3,4,5];  交换之后在这里还是满足降序排列
>        //[5,4,3,2,1]--->[1,2,3,4,5]                             直 接进行交换就可以在这里哈呢
>        //存在上述这两种情况 找到或者没有找到 我们就是直接进行双指针交换 时间复杂度O(nlogn) 要不进行排序时间复杂度O(NLOGN)
>        sort(nums, left, right);
>        return nums;
>    }
>
>    private void sort(int[] nums, int left, int right) {
>        while (left < right) {
>            swap(nums, left, right);
>            left++;
>            right--;
>        }
>    }
>
>    private void swap(int[] nums, int i, int j) {
>        int temp = nums[i];
>        nums[i] = nums[j];
>        nums[j] = temp;
>    }
>```
>
>



## [全排列  II](https://leetcode-cn.com/problems/permutations-ii/)

>```
>输入：nums = [1,2,3]
>输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
>```
>
>首先这种类似于排列带有重复数字或者就是字母 我们首先就是要进行**排序 方便后续进行剪枝**
>
>1. 回溯+剪枝1(`boolean[] visited`数组是否拜访过) +
>2. 剪枝2 先进行排序 (`if(i>0 && nums[i]==nums[i-1] && visited[i-1]==false)`)重复元素进行剪枝。
>
>----
>
>1. 时间复杂度：*O*(*n*×*n*!)，其中 *n* 为序列的长度
>2. 空间复杂度：标记是否拜访过 O(N)      同时在递归的时候栈深度会达到 O(n)，因此总空间复杂度为 O(n + n)=O(2n)



## [第K个排列-hard](https://leetcode-cn.com/problems/permutation-sequence/)

>```xml
>给出集合 [1,2,3,...,n]，其所有元素共有 n! 种排列。 按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：
>"123"
>"132"
>"213"
>"231"
>"312"
>"321"
>给定 n 和 k，返回第 k 个排列。
>```
>
>思路1：如果在这里进行回溯 ， 在这里返回第K个排列  这种时间复杂度太大是 O(n*n!)
>
>思路2：进行数学问题求解  



## [下一个排列](https://leetcode-cn.com/problems/next-permutation/)

>```
>输入：nums = [1,2,3]
>输出：[1,3,2]          
>```
>
>思路：三步走 如果不走第2不 那么就是直接走第三步合并都是一样的  第三步使用双指针进行排序减少时间复杂度
>
>```xml
>1. 首先从后向前查找第一个顺序对 (i,i+1)，满足 a[i] < a[i+1]。这样「较小数」即为 a[i]。此时 [i+1,n) 必然是下降序列。
>
>2. 如果找到了顺序对，那么在区间 [i+1,n) 中从后向前查找第一个元素 j 满足 a[i] < a[j]。这样「较大数」即为 a[j]。
>
>3. 交换 a[i]与 a[j]，此时可以证明区间 [i+1,n) 必为降序。我们可以直接使用双指针反转区间 [i+1,n) 使其变为升序，而无需对该区间进行排序。
>```
>
>-----
>
>1. 时间复杂度：O(N) 只需要两趟扫描和一次反转
>2. 空间复杂度：只需要常数的空间存放若干变量。





## [无重复字符串的排列组合](https://leetcode-cn.com/problems/permutation-i-lcci/)

>```
> 输入：S = "ab"
> 输出：["ab", "ba"]
>```
>
>1. 回溯+剪枝（`boolean[] visited`数组进行剪枝 判断是否拜访过）
>2. 利用一个`StringBuilder`来添加字符
>
>------
>
>1. 时间复杂度：*O*(*n*×*n*!)，其中 *n* 为字符串的长度
>2. 空间复杂度：标记是否拜访过 O(N)      同时在递归的时候栈深度会达到 O(n)，因此总空间复杂度为 O(n + n)=O(2n)



## [有重复字符串的排列](https://leetcode-cn.com/problems/permutation-ii-lcci/)

>```
> 输入：S = "qqe"
> 输出：["eqq","qeq","qqe"]
>```
>
>1. 回溯+剪枝（`boolean[] visited`数组进行剪枝 判断是否拜访过）
>2. 剪枝2 重复先进行排序  (`if(i>0 && nums[i]==nums[i-1] && visited[i-1]==false)`)重复元素进行剪枝。
>
>-----
>
>1. 时间复杂度：*O*(*n*×*n*!)，其中 *n* 为字符串的长度
>2. 空间复杂度：标记是否拜访过 O(N)      同时在递归的时候栈深度会达到 O(n)，因此总空间复杂度为 O(n + n)=O(2n)



## [字母大小写全组和](https://leetcode-cn.com/problems/letter-case-permutation/)

>```
>输入：S = "a1b2"
>输出：["a1b2", "a1B2", "A1b2", "A1B2"]
>```
>
>1. 思路：首先确定这个是组和问题： 不是排列问题  我们需要`int index`这个变量来维持组和形式 且 没有`for循环` 
>2. 其次：分两种情况 一种是数字不动继续回溯增加和删除    一种是字母两种情况进行递归
>
>------
>
>1. 时间复杂度：*O*(2^*N*∗*N*)，其中 N 是 `S` 的长度。
>
>2. 空间复杂度：O(2^N * N))



## [子集](https://leetcode-cn.com/problems/subsets/)

>```
>输入：nums = [1,2,3]
>输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
>```
>
>1. 回溯  这个就是相当于组和问题 在这里就是`int index`变量来维持这个组和问题呗   这里边是带有`for`循环 跟字母大小全组和不一样
>2. 迭代：遇到一个数就把所有子集加上该数组成新的子集，遍历完毕即是所有子集  前提是需要加入一个空的子集；迭代方法比较巧妙
>
>-------
>
>1. 时间复杂度：*O*(n*2^n)，一共 2^n 个状态，每种状态需要 O(n)*的时间来构造子集
>
>2. 空间复杂度：O(n)。临时数组 t的空间代价是 O(n)，递归时栈空间的代价为 O(n)。



## [子集 II](https://leetcode-cn.com/problems/subsets-ii/)

>```
>输入：nums = [1,2,2]
>输出：[[],[1],[1,2],[1,2,2],[2],[2,2]]
>```
>
>1. 首先就是需要进行排序。 
>2. 组合形式在这里需要 `int index`变量
>3. 重复元素去重复 需要`boolean[] visited`--->`if(i>0 && nums[i]==nums[i-1] && visited[i-1]==false)` 
>4. 回溯进行调用
>
>------
>
>1. 时间复杂度：*O*(n*2^n)，一共 2^n 个状态，每种状态需要 O(n)*的时间来构造子集 ， 每个子集加入答案时需要拷贝一份。排序O(nlogn)；
>
>2. 空间复杂度：O(n)。临时数组 t的空间代价是 O(n)，递归时栈空间的代价为 O(n)。



## [划分为k个相等的子集](https://leetcode-cn.com/problems/partition-to-k-equal-sum-subsets/)

>跟上述子集的思路是差不多呢 
>
>这个就是比较难





## [复原 IP 地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

>```
>输入：s = "25525511135"
>输出：["255.255.11.135","255.255.111.35"]    0--255之间 并且不能有特殊符号
>```
>
>1. 首先就是回溯+剪枝    
>2. 递归退出条件：点数量 `.` 作为递归退出条件  并且判断第四段字符串是否合法
>3. `for`循环进行回溯  并且判断当前段字符串是否合法
>4. 判断是否单独开一个函数来判断
>
>-----
>
>时间复杂度：根据当前字符串长度  



## [分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)

>```
>输入：s = "aab"
>输出：[["a","a","b"],["aa","b"]]   分割成子串 并时成回文串 同时不能改变相对顺序
>```
>
>1. 也是组合问题 跟上边复原IP地址就是很像  
>2. `for(int i=index; i<s.length(); i++)`  进行字符串截取并判断是否是回文串 如果不是继续循环 
>3. 如果当前是回文串加入`list` 并继续递归
>
>-----
>
>时间复杂度：O(n* 2^n)  每一个位置可以拆分也可以不拆分 尝试可以拆分时间复杂度O(2^N) 判断每一个子串是否是回文串 时间复杂度为O(N)
>
>空间复杂度：O(N) 调用栈的高度 



## [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

>```
>输入：digits = "23"
>输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
>```
>
>思路：这个数字重复和不重复都可以 没有区别  同时我们必须要按照数字给定的顺序来做组合   说到组合指定要使`int index`变量
>
>1. 首先数字对应的字母 我们需要用`HashMap`来封装一下呢 
>2. 其次每遇到一个数字 就`for (int j=0; i<=3; j++)` 一个数字对应三个字母 还是在需要for循环 之后在这里用`StringBuilder`来添加 递归
>
>-----
>
>1. 时间复杂度：O(3^m * 4^n)   m是3个字母的数字个数  n是4个字母的数字个数
>2. 空间复杂度：递归调用层数 O(M+N)  这里边不对吧



## [组合](https://leetcode-cn.com/problems/combinations/)

>```xml
>给定两个整数 n 和 k，返回范围 [1, n] 中所有可能的 k 个数的组合。
>你可以按 任何顺序 返回答案。
>输入：n = 4, k = 2
>输出：
>[
>  [2,4],
>  [3,4],
>  [2,3],
>  [1,2],
>  [1,3],
>  [1,4],
>]
>```





## [组合总和](https://leetcode-cn.com/problems/combination-sum/)

>```xml
>输入: candidates = [2,3,6,7], target = 7
>输出: [[7],[2,2,3]]
>```

## [组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

>相比于 组合总和这里就是带有重复数字呗 

## [组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

>```
>输入: k = 3, n = 9       数组中存在1-9的数字
>输出: [[1,2,6], [1,3,5], [2,3,4]]
>```



## [火柴拼正方形](https://leetcode-cn.com/problems/matchsticks-to-square/)

>```xml
>输入: [1,1,2,2,2]
>输出: true
>```
>
>这个一定要先做一下判断之后在进行回溯
>
>1. 并且要进行排序
>2. 创建一个 `new int[4]` 并对数组下表进行内容添加
>3. 先对大的元素进行添加  可以减少回溯情况

## 二维数组笛卡尔乘积

>```xml
>{{1,2},{3,4},{5}}  输出  [1,3,5] [1,4,5] [2,3,5] [2,4,5] 
>```
>
>思路  这个相当于去全排列 需要boolean数组  又需要不能重复
>
>```java
>private List<List<Integer>> res;
>
>private List<List<Integer>> dfs(int[][] nums) {
>   res = new LinkedList<>();
>   int len = nums.length;
>   boolean[][] visited = new boolean[len][];
>   for (int i = 0; i < nums.length; i++) {
>       visited[i] = new booleasn[nums[i].length];
>   }
>   boolean[] row = new boolean[len];
>   traceBack(nums, 0, new LinkedList<>(), row, visited);
>   return res;
>}
>
>private void traceBack(int[][] nums, int ro, LinkedList<Integer> list, boolean[] row, boolean[][] visited) {
>
>  if (list.size() == nums.length) {
>  res.add(new LinkedList<>(list));
>       return;
>   }
>   for (int i = ro; i < nums.length; i++) {           
>       if (row[i]) continue;
>       row[i] = true;
>       for (int j = 0; j < nums[i].length; j++) {
>           if (visited[i][j]) continue;
>           //这里边报空指针异常了倍
>           list.addLast(nums[i][j]);
>           visited[i][j] = true;
>           traceBack(nums, i + 1, list, row, visited);		//这个i+1 在这里就是非常重要呗  不让他重复进入一维数组里边·		
>           list.removeLast();
>           visited[i][j] = false;
>       }
>       row[i] = false;
>   }
>}
>```



## 二维字符串数组笛卡尔乘积  字节一面题

>跟上述思路差不多在这里哈呢 
>
>1. 注意对应的数组初始化长度一定要对应上  否则就会报空指针异常
>
>```JAVA
>import java.util.*;
>public class Main {
>    public static void main(String[] args) {
>        ArrayList<ArrayList<String>> list=new ArrayList<>();
>        ArrayList<String> s=new ArrayList<>();
>        s.add("1");
>        s.add("2");
>        s.add("3");
>        ArrayList<String> s1=new ArrayList<>();
>        s1.add("a");
>        s1.add("b");
>        ArrayList<String> s2=new ArrayList<>();
>        s2.add("A");
>        list.add(s);
>        list.add(s1);
>        list.add(s2);
>        ArrayList<String> result=Product(list);
>        System.out.println(result);
>    }
>    private static ArrayList<String> res=new ArrayList<>();
>    private static ArrayList<String> Product(ArrayList<ArrayList<String>> list) {
>        
>        int len=list.size();
>        String[][] strs=new String[len][];
>        
>        for(int i=0; i<len; i++){
>            ArrayList<String> str=list.get(i);
>            strs[i] = new String[str.size()];
>            for(int j=0; j<str.size(); j++){
>                strs[i][j]=str.get(j);
>            }
>        }
>        boolean[] row=new boolean[len];
>        boolean[][] visited=new boolean[len][];
>        for(int i=0; i<len; i++){
>            visited[i]=new boolean[strs[i].length];
>        }
>        
>        dfs(strs,0,new StringBuilder(),row,visited);
>        return res;
>    }
>   //这个函数就是重点呢哈 
>    private static void dfs(String[][] strs,int begin,StringBuilder sb, boolean[] row, boolean[][] visited){
>        if(sb.length()==strs.length){
>            res.add(sb.toString());
>            return;
>        }
>        for(int i=begin; i<strs.length; i++){
>            if(row[i]==true) continue;
>            row[i]=true;
>            for(int j=0; j<strs[i].length; j++){
>                sb.append(strs[i][j]);   //1 a  A B
>                visited[i][j]=true;
>                dfs(strs,i+1,sb,row,visited);
>                sb.deleteCharAt(sb.length()-1);
>                visited[i][j]=false;
>            }
>            row[i]=false;
>        }
>    }
>}
>```







# ==---------------------------------------------------------------DFS==

## [N 皇后](https://leetcode-cn.com/problems/n-queens/)

>N皇后：使其中任意两个皇后都不同列、同行和在一条斜线上
>
>------
>
>1. 首先这里边直接暴力求解 n个for循环就是可以解决
>2. 使用递归解法： 重第0行开始摆放-->判断哪个列可以进行摆放--->循环第1行 看哪个列可以进行摆放
>3. 这里边我们就是可以使用一维数组来进行空间压缩 `result[]=new int[n]`  数组下标代表行 数组内容代表值 可以节省一下空间
>4. 如何判断不在同一行上、同一列上、同一对角线上呢  这个是解决问题的关键？
>
>```java
>    private boolean isAccessible(int row, int column, int n) {
>        int left = column - 1;  // 对角线左上
>        int right = column + 1; // 对角线右上
>        // 从当前行的上一行开始，向上遍历 （没有必要判断当前行的下面几行了，因为下面几行肯定没有放皇后啊）
>        for (int i = row - 1; i >= 0; i--) {
>            if (result[i] == column) return false;   // 当前列上不能有皇后
>            if (left >= 0 && result[i] == left) return false;  // 左上对角线上不能有皇后
>            if (right < n && result[i] == right) return false; // 右上对角线上不能有皇后
>            left--;
>            right++;
>        }
>        return true;
>    }
>```
>
>-------
>
>1. 时间复杂度：O(N!)，其中 N 是皇后数量。
>
>2. 空间复杂度：O(N)，其中 N 是皇后数量。空间复杂度主要取决于递归调用层数、记录每行放置的皇后的列下标的数组以及三个集合，递归调用层数不会超过 N，数组的长度为 N，每个集合的元素个数都不会超过 N。







## [二维矩阵中的最长递增路径](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)

>给定一个 `m x n` 整数矩阵 `matrix` ，找出其中 **最长递增路径** 的长度。 只可以上下左右四个方向移动呗
>
>--------
>
>思路：
>
>1. Dfs + 备忘录： 遍历数组每个节点， 以该节点为起始节点 并进行递归四个方向遍历
>2. 同时用一个二维数组 来记录对应位置的最长递增路径长度 这里边也是后续进行剪枝的手段。
>
>--------
>
>1. 时间复杂度：O(mn)，其中 m和 n 分别是矩阵的行数和列数。深度优先搜索的时间复杂度是 O(V+E)，其中 V是节点数，E 是边数。在矩阵中，O(V)=O(mn)，O(E)≈O(4mn)=O(mn)。
>
>2. 空间复杂度：O(mn)，其中 m 和 n 分别是矩阵的行数和列数。空间复杂度主要取决于缓存和递归调用深度，缓存的空间复杂度是 O(mn) 递归调用深度不会超过 mn.



## [单词搜索](https://leetcode-cn.com/problems/word-search/)

>给定一个 `m x n` 二维字符网格 `board` 和一个字符串单词 `word` 。如果 `word` 存在于网格中，返回 `true` ；否则，返回 `false` 。
>
>------
>
>1. 遍历二维数组，当遇到单词第一个字母相等的时候 进行递归判断剩余的字母是否在二维数组当中连续呗
>
>------
>
>时间复杂度：O(mn * 3^L)  就是当一个单词相等了 我们只需要判断四个方向  其中L是单词长度 
>
>空间复杂度：O(mn) 开辟一个visited数组 用来确定是否拜访过 



## [机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

>地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0] `的格子开始移动。 取余数+相除
>
>------
>
>1. 直接重起始点开始进行递归就是可以  
>2. 返回条件数组别越界， 并且判断是不是访问过。 访问过了后续就不需要在进行访问了 在这里
>
>----
>
>1. 时间复杂度：O(mn)，一共有 O(mn) 个状态需要计算，每个状态递推计算的时间复杂度为 O(1)，所以总时间复杂度为 O(mn)
>2. 空间复杂度：O(mn)，需要一个`boolean[][] visited`来判断是否拜访过。



## [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

>由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，请你计算网格中岛屿的数量。
>
>------
>
>1. 思路：遍历岛这个二维数组，如果当前数为1，则进入感染函数 并且 将岛个数+1
>
>2. 感染函数：其实就是一个递归标注的过程，它会将所有相连的1都标注成2。这样就避免了遍历过程中的重复计数的情况，一个岛所有的1都变成了2后，遍历的时候就不会重复遍历了。
>3. 这里边直接对原数组进行改动 就不用在需要一个 `boolean[][]`数组来判断是否是走过   
>
>------
>
>时间复杂度：O(MN)，其中 M 和 N 分别为行数和列数。
>
>空间复杂度：O(MN)，在最坏情况下，整个网格均为陆地，深度优先搜索的深度达到 M N



## [二维矩阵中的最长递增路径](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)

>给定一个 `m x n` 整数矩阵 `matrix` ，找出其中 **最长递增路径** 的长度。 只可以上下左右四个方向移动呗
>
>--------
>
>思路：
>
>1. Dfs + 备忘录： 遍历数组每个节点， 以该节点为起始节点 并进行递归四个方向遍历
>2. 同时用一个二维数组 来记录对应位置的最长递增路径长度 这里边也是后续进行剪枝的手段。
>
>--------
>
>时间复杂度：O(mn)，其中 m和 n 分别是矩阵的行数和列数。深度优先搜索的时间复杂度是 O(V+E)，其中 V是节点数，E 是边数。在矩阵中，O(V)=O(mn)，O(E)≈O(4mn)=O(mn)。
>
>空间复杂度：O(mn)，其中 m 和 n 分别是矩阵的行数和列数。空间复杂度主要取决于缓存和递归调用深度，缓存的空间复杂度是 O(mn) 递归调用深度不会超过 mn.



##  [斐波那契数列--累加数](https://leetcode-cn.com/problems/additive-number/)

>```xml
>输入: "112358"
>输出: true 
>解释: 累加序列为: 1, 1, 2, 3, 5, 8 。1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8
>```
>
>思路：
>
>1. 双重for循环  
>2. `for` 循环之后进行截取字符串并判断并递归进行判断是否是斐波那契数列



## [汉诺塔问题](https://leetcode-cn.com/problems/hanota-lcci/)

# ==---------------------------------------------------------------链表==

# ==链表反转==

## [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

>重点： 递归  递归版本在这里就是写出来了呢哈   这里边就是链表翻转呗 就是在这里哈呢  所以你就说说这个呗
>
>```java
>class Solution {
>    public ListNode reverseList(ListNode head) {
>        //通过 递归 但是要把递归的思路就是说清楚 
>   if(head==null || head.next==null) return head;
>     
>   ListNode res = reverseList(head.next);   //head.next==5退出循环了  head==4   res=5
>     
>   head.next.next=head;        // 5-->4
>     
>   head.next=null;     //4-->null
>     
>   return res;
>     }
>    }
>```



## [反转链表 II 重m到n反转](https://leetcode-cn.com/problems/reverse-linked-list-ii/)



## [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)



## [重排链表](https://leetcode-cn.com/problems/reorder-list/)

>思路 找到链表中间节点
>
>```java
>while(fast!=null      && fast.next!=null)      //这个是找到偶数节点中的后一个
>while(fast.next!=null && fast.next.next!=null) //这种是找到偶数节点中前一个节点呢
>```
>
>思路：
>
>1. 寻找到链表中间节点
>2. 反转链表
>3. 合并这一步需要看链表进行好好想一下呢



## [回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

>在这里就是跟重排链表差不多呢 
>
>1. 找到中间节点
>2. 进行反转      记住要把前驱节点指向当前头结点置为Null
>3. 两个链表进行判断





## [奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

>思路：
>
>1. 需要一次遍历就是进行完事  所以奇数连接奇数呗  偶数连接偶数  主要两个三个额外变量
>2. 复制引用两个头结点呗 
>3. `while(even!=null && even.next!=null)`  不需要判断odd奇数节点 指定是在偶数节点前边呗





## [相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

>```xml
>给定两个头结点 在这里就是找到相交链表节点呗
>```
>
>**若相交，链表A： a+c, 链表B : b+c. a+c+b+c = b+c+a+c 。则会在公共处c起点相遇。若不相交，a +b = b+a 。因此相遇处是NULL**
>
>因为有你在我看到未来  



## [环形链表 找到环点 美团一面](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

>判断链表是否是环形链表  并找出环节点呗
>
>1. 进行数学推导呗  https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/
>2. 快慢双指针在这里进行求解呗  



# ==删除节点==



## [删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

>O(n) 时间复杂度  就是简单双指针找到待删除节点的前驱节点就完事了



## [删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

>这种就是找val值在这里进行删除  
>
>创建一个虚拟头结点  双指针前行 找到代删除节点的前驱节点就可以了呢



## [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

>也是类似于双指针  就是往前边走就好了呢 在这里哈呢



## [删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

>在这里 就是没有做出来呢哈 那天回顾一下再做  老是爆出空指针异常 在好好想想处理一下呢
>
>





# ==合并、排序、相加链表==

## [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)



## [合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

>思路：  这边就是需要建立堆的数据结构呗 并且我们需要重写堆在这里的数据结构呢 内部是维护链表 
>
>```java
>        PriorityQueue<ListNode> minHeap = new PriorityQueue<>(new Comparator<ListNode>() {
>            @Override
>            public int compare(ListNode o1, ListNode o2) {      //建立一个最小堆
>                return o1.val - o2.val;
>            }
>        });
>```



## [对链表进行插入排序](https://leetcode-cn.com/problems/insertion-sort-list/)

## [排序链表 快排 归并](https://leetcode-cn.com/problems/sort-list/)

>首先在这里就是进行归并排序 对链表进行排序呗  重点呢  主要就是在这里进行归并排序     快速排序进行递交了
>
>时间复杂度：O(nlogn)，其中 n 是链表的长度。
>
>空间复杂度：O(logn)，  其中  n 是链表的长度。空间复杂度主要取决于递归调用的栈空间。



## [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

>正常重头到尾进行相加  双指针进行遍历  以及需要一个进位标志在这里就是可以了呢





## [两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

>类似于数字相加   
>
>如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。
>
>重点： 不能使用反转链表  所以需要一种数据结构：栈   但是最后合并的时候需要对头节点进行迭代呗
>
>1. 思路  创建两个栈 把链表压入到栈中
>2. 创建一个尾结点进行迭代  之后相加链表产生新的节点对尾结点头插  尾结点再次更新为当前节点就是可以了呢





# ==---------------------------------------------------------------二叉树==

# ==遍历==

## 3种遍历方式

>“遍历”的本质是对内存的有序访问，失去了访问顺序，即便你用各种数据结构恢复了这个次序，遍历本身也显得毫无意义
>
>#### [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
>
>#### [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
>
>#### [ 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/) 



## [从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

>`list` 一个队列就是搞定了呢



## [从上到下打印二叉树 II 分层](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)



## [ 二叉树Z字形遍历](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

>1. 利用 返回集合做文章类型呗  利用他的下表
>2. 来判断前边插入 还是后边插入



## [二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)

>**存放树的索引来实现 判断二叉树最大宽度呗**
>
>     1. 根据满二叉树的特性  在这里就是每个节点都是简历索引 
>     2. 当前父节点是 `index   那么左节点2*index  右节点 2*index+1`  
>     3. 每遍历一次 我们在这里就是更新一下这个节点



## [二叉树的堂兄弟节点](https://leetcode-cn.com/problems/cousins-in-binary-tree/)

>层序遍历 
>
>1. 只要在一层 不在一层直接返回false
>2. 在一层 在判断一下特殊情况  不是相同的父节点就可以了呢
>3. `利用HashSet` 来做这个比较号  时间复杂度O(1)





# ==二叉树构造==



## [填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

><img src="https://assets.leetcode.com/uploads/2019/02/14/116_sample.png" alt="img" style="zoom:33%;" />
>
>思路：
>
>层序遍历 ： 使用队列每遍历一层 我们就是连接一层呗 
>
>----
>
>递归：         左连接右呗 





## [填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

><img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png" alt="img" style="zoom:33%;" />
>
>这种情况就不是满二叉树  所以在这里需要进行区别呢呗
>
>- 层序遍历 灵活使用`LinkedList`中的方法
>- 递归： 这个就是不好整 因为就是正常的二叉树 要考虑最后 一层的极端情况呗 在这里哈呢 而且这个递归写的经历非常棒呗



## [从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## [从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

## [从前序与后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

>重点：根据前序遍历和后续遍历不能唯一确定一个二叉树
>
>例如  `前序AB`   ` 后续BA`  这里边就是可以有两种解决办法 所以在做这个题的时候 我们就是确定唯一一个策略 就是尽量先构造左子树呗  就是这个样子



## [二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

>这里边就是需要我们来定制规则呗    **利用前序遍历， 递归对二叉树进行拆解， 递归对二叉树进行拼接**
>
>树-->string  序列化
>
>string->树   反序列化





## [二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)

><img src="https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg" alt="img" style="zoom:33%;" />
>
>1. 先找到左子树当中的最右边节点 是根的右节点 

## [二叉搜索树展开为双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

>不会  这里边需要递归吧



# ==数组、链表与二叉搜索树==

## [给定数组判断是否是二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

>```
>     5
>    / \
>   2   6
>  / \
> 1   3
> 输入: [1,3,2,6,5]
> 输出: true
>```
>
>思路：
>
>1. 二叉搜索树后续遍历 是左右父  如果是正序遍历没有什么特点  但是在这里如果是倒叙遍历 我们就是可以使用单调栈的思想呗 
>2. 翻转先序遍历又是root->right->left的
>3. 右子树 value值遍历过程中 是越来越大的，一旦出现了value小于栈顶元素value的时候，就表示要开始进入左子树了
>4. 只要栈顶元素还比当前节点大，就表示还是右子树，要移除，因为我们要找到这个左孩子节点直接连接的父节点，也就是找到这个子树的根，只要栈顶元素还大于当前节点，就要一直弹出，直到栈顶元素小于节点，或者栈为空。栈顶的上一个元素就是子树节点的根。
>5. 接下来，数组继续往前遍历，之后的左子树的每个节点，都要比子树的根要小，才能满足二叉搜索树，否则就不是二叉搜索树。



## [前序遍历数组构造二叉搜索树](https://leetcode-cn.com/problems/construct-binary-search-tree-from-preorder-traversal/)

><img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/03/08/1266.png" alt="img" style="zoom:33%;" />
>
>```
>输入：[8,5,1,7,10,12]
>输出：[8,5,10,1,7,null,12]
>```
>
>思路： 先固定父节点 判断左子树的节点有一个 进行递归在构造  之后判断右子树节点有几个 在进行递归构造



## [将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

>给你一个整数数组 `nums` ，其中元素已经按 **升序** 排列，请你将其转换为一棵 **高度平衡** 二叉搜索树。
>
>`int mid=begin + (end-begin)/2`    因为这里边构造就是有多种情况  选择中间点构造根元素在这里就是可以了呢 之后递归进行构造



## [有序链表转换二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

>在这里其实跟有序数组在这里差不多呢   但是处理起来细节比较多    
>
>1. 寻找链表中间节点
>2. 我们还需要左闭右开区间   对应找到链表中间节点  
>3. `private ListNode getMidListNode(ListNode left, ListNode right) `  其中初始传递是`head, null`  非常重要呗



## [数组构造最大二叉树](https://leetcode-cn.com/problems/maximum-binary-tree/)

>跟有序数组构造成二叉搜索树 意思差不多    只不多这里边最大二叉树的定义不一样





# ==树的验证==





## [二叉搜索树的验证](https://leetcode-cn.com/problems/validate-binary-search-tree/)

>给定头结点 在这里判断是不是二叉搜索树呗
>
>思路：
>
>1. 二叉搜索树中序遍历是升序  所以可以在这里做文章  
>2. 递归进行遍历   需要考虑上下界 但是这种办法就是考虑的点就是有点多被   **而且第三层以后的节点就是上下界都是需要同时考虑的被** 上界和下届的边界问题同时需要考虑 是采用Integer  还是Long类型被  因为树的节点就是可能存在最大Integer.MAX_VALUE 或者就是Integer.MIN_VALUE

## [平衡二叉树的验证](https://leetcode-cn.com/problems/balanced-binary-tree/)

>这个题  两种办法：
>
>​			 1.  重上到下		：这种办法就是时间复杂度非常大 就是没有进行剪支 逻辑简单  求树得最大深度就是可以了呢
>
>​			 2.  重下到上		：重最底下进行判断  保留前边得结果了 就是进行了剪支 这种实现就是可以得呢  **三刷得时候需要会这个**



## [对称的二叉树的验证](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

>左右子树进行对称呗  在这里哈呢
>
>` return dfs(root.left,root.right);`   重启一个函数在这里就是进行递归呗



## [完全二叉树的检验](https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree/)

>思路：
>
>1. 使用一个队列
>2. 添加进去头结点  如果不为null 我么就是加入左右节点  直到弹出节点为Null
>3. 之后再判断队列里边的节点  如果有不为null  我们直接就是返回false



## [B树是否是A树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

>思路：
>
>1. 先生成一个新函数
>2. 遇到相等的值 我们在新函数里边递归  判断是否符合





# ==深度、祖先==



## [二叉树的最大深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

## [二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)



## [完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

> 除了最后一层不是满的 其余层都是满的 
>
>1. 所以在这里进行优化一下呢
>2. 最后一层在进行递归

## [二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

## [二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

>重点： 判断递归当中的`if else if`走了几遍   答案：最多三遍



# ==路径==



## [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

>直径长度： 可能就是不存在连接根节点的地方呗 所以需要怎么判断    写了好多遍 
>
>重点：思路： 递归判断每一个节点的左右最大深度呗 用一个变量来维持就是可以了

## [路径总和 boolean](https://leetcode-cn.com/problems/path-sum/)

## ==[路径总和 List 重点 ](https://leetcode-cn.com/problems/path-sum-ii/)==

>在这里就是可以使用回溯 记住回溯模板  跟上边两道题就是很像
>
>时间复杂度： O(N^2)    最坏的时候上层退化成链表 底部是满二叉树 每条路径都符合
>
>空间复杂度： O(N)



## [路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

>存在两个问题： 1. 可以不重根节点开始
>
>​							2.可以不到叶子节点 		     怎么解决这两个问题就是解决问题的关键呗
>
>解题思路：
>
>​						   1.双重递归 先序遍历每个节点  + 在递归遍历这个节点得往下是否满足
>
>​						   2.递归 + 前缀(`HashMap`) 优化时间复杂度





## [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

>维持变量  返回值  这两个就是一定要仔细想一想 
>
>难点： 都是可以不重根节点出发 而且都需要维持一个变量



## [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)



## [最长同值路径](https://leetcode-cn.com/problems/longest-univalue-path/)

>重点：跟上边就是差不多  思想就是一样的我们要好好想一想 返回值 和 维持变量呗 在这里哈呢



## [根节点出发打印所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)



## [求根节点到叶节点数字之和](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

>```xml
>输入：root = [1,2,3]
>输出：25
>解释：
>从根到叶子节点路径 1->2 代表数字 12
>从根到叶子节点路径 1->3 代表数字 13
>因此，数字总和 = 12 + 13 = 25
>```





# ==二叉搜索树==





## [二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

## [不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)

## [不同的二叉搜索树 II](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)

## [二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

## [二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)



## [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)





# ==---------------------------------------------------------------排序==

>![img](https://images2017.cnblogs.com/blog/849589/201710/849589-20171015233043168-1867817869.png)
>
>- 前三种简单的算法必须就是信手捏来 希尔排序是插入排序的升级版  
>- 归并排序 快速排序 堆排序 重点
>- 归并排序思想：递归到剩下一个元素 再数组有序的情况下进行合并	  递归剩最后一个元素再合并   		 所以归并排序重无序--->部分有序----->有序 
>- 快速排序思想：找到轴点元---->递归左右--->再找轴点                  直到轴点就是只剩下一个元素         		  所以快速排序是重无序--->部分有序--->有序
>



# ==十大排序算法==



## 快速排序

>1. 基本思路：快速排序每一次都排定一个元素（这个元素呆在了它最终应该呆的位置），然后递归地去排它左边的部分和右边的部分，依次进行下去，直到数组有序；
>2. 算法思想：分而治之（分治思想），与「归并排序」不同，「快速排序」在「分」这件事情上不想「归并排序」无脑地一分为二，而是采用了 partition 的方法   因此就没有「合」的过程。
>
>```xml
>快速排序最好情况nlgn  最坏情况n^2/2
>最好情况： 恰好每次5 5分  一共递归需比较n次， 递归深度lgn
>最坏情况: 以排序数组  笔记次数 n+(n-1)+(n-2)+(n-3)+...  ==(n)*(n-1)/2
>```
>
>
>
>```java
>import.java.util.*;
>
>public class Main {
>   private int[] quickSort(int[] nums) {
>        int len = nums.length;
>       if (len == 0) return null;
>        sort(nums, 0, len - 1);
>        return nums;
>    }
>    private void sort(int[] nums, int left, int right) {
>       if (left > right) return;
>        int pivotIndex = partition(nums, left, right);  //这里边就是返回一个轴点元素索引呢 在这里哈呢
>       sort(nums, left, pivotIndex - 1);
>       sort(nums, pivotIndex + 1, right);
>    }
>    private int partition(int[] nums, int left, int right) {
>        int randomIndex = new Random().nextInt(right - left + 1) + left;
>        swap(nums, randomIndex, left);
>        int pivotNum = nums[left];
>        int le = left;
>        for (int i = left + 1; i <= right; i++) { //  i===left+1 记住了哈呢
>            if (nums[i] < pivotNum) {
>                le++;                             //这里边就是必须先让le进行++操作呗 在这里哈呢
>                if (i != le) swap(nums, i, le);
>            }
>        }
>       swap(nums, le, left);
>        return le;
>    }
>    private void swap(int[] nums, int i, int j) {
>        int temp = nums[i];
>       nums[i] = nums[j];
>        nums[j] = temp;
>    }
>}
>```



## 堆排序

>```xml
>堆排序是选择排序的优化，选择排序需要在未排定的部分里通过「打擂台」的方式选出最大的元素（复杂度 O(N)），而「堆排序」就把未排定的部分构建成一个「堆」，这样就能以 O(logN) 的方式选出最大元素；
>```
>
>```java
>public class Solution {
>
>//这里边是最小堆 在这里哈呢  
>public int[] sortArray(int[] nums) {
>   int len = nums.length;
>   // 将数组整理成堆
>   heapify(nums);
>
>   // 循环不变量：区间 [0, i] 堆有序
>   for (int i = len - 1; i >= 1; ) {
>       // 把堆顶元素（当前最大）交换到数组末尾
>       swap(nums, 0, i);
>       // 逐步减少堆有序的部分
>       i--;
>       // 下标 0 位置下沉操作，使得区间 [0, i] 堆有序
>       siftDown(nums, 0, i);
>   }
>   return nums;
>}
>
>/**
>    * 将数组整理成堆（堆有序）
>    *
>    * @param nums
>    */
>   private void heapify(int[] nums) {
>       int len = nums.length;
>       // 只需要从 i = (len - 1) / 2 这个位置开始逐层下移
>       for (int i = (len - 1) / 2; i >= 0; i--) {
>           siftDown(nums, i, len - 1);
>       }
>   }
>
>   /**
>    * @param nums
>    * @param k    当前下沉元素的下标
>    * @param end  [0, end] 是 nums 的有效部分
>    */
>   private void siftDown(int[] nums, int k, int end) {
>       while (2 * k + 1 <= end) {
>           int j = 2 * k + 1;
>           if (j + 1 <= end && nums[j + 1] > nums[j]) {
>               j++;
>           }
>           if (nums[j] > nums[k]) {
>               swap(nums, j, k);
>           } else {
>               break;
>           }
>           k = j;
>       }
>   }
>
>   private void swap(int[] nums, int index1, int index2) {
>       int temp = nums[index1];
>       nums[index1] = nums[index2];
>       nums[index2] = temp;
>   }
>}
>```



## 归并排序

>- 基本思路：借助额外空间，递归分开到最后一个元素。 合并两个有序数组，得到更长的有序数组。
>- 算法思想：分而治之（分治思想）。
>
>```java
>public class Solution {
>    // 归并排序
>
>    /**
>     * 列表大小等于或小于该大小，将优先于 mergeSort 使用插入排序
>     */
>    private static final int INSERTION_SORT_THRESHOLD = 7;
>
>    public int[] sortArray(int[] nums) {
>        int len = nums.length;
>        int[] temp = new int[len];
>        mergeSort(nums, 0, len - 1, temp);
>        return nums;
>    }
>
>    /**
>     * 对数组 nums 的子区间 [left, right] 进行归并排序
>     * @param nums
>     * @param left
>     * @param right
>     * @param temp  用于合并两个有序数组的辅助数组，全局使用一份，避免多次创建和销毁
>     */
>    private void mergeSort(int[] nums, int left, int right, int[] temp) {
>        // 小区间使用插入排序
>        if (right - left <= INSERTION_SORT_THRESHOLD) {
>            insertionSort(nums, left, right);
>            return;
>        }
>
>        int mid = left + (right - left) / 2;
>        // Java 里有更优的写法，在 left 和 right 都是大整数时，即使溢出，结论依然正确
>        // int mid = (left + right) >>> 1;
>
>        mergeSort(nums, left, mid, temp);
>        mergeSort(nums, mid + 1, right, temp);
>        // 如果数组的这个子区间本身有序，无需合并
>        if (nums[mid] <= nums[mid + 1]) {
>            return;
>        }
>        mergeOfTwoSortedArray(nums, left, mid, right, temp);
>    }
>
>    /**
>     * 对数组 arr 的子区间 [left, right] 使用插入排序
>     *
>     * @param arr   给定数组
>     * @param left  左边界，能取到
>     * @param right 右边界，能取到
>     */
>    private void insertionSort(int[] arr, int left, int right) {
>        for (int i = left + 1; i <= right; i++) {
>            int temp = arr[i];
>            int j = i;
>            while (j > left && arr[j - 1] > temp) {
>                arr[j] = arr[j - 1];
>                j--;
>            }
>            arr[j] = temp;
>        }
>    }
>
>    /**
>     * 合并两个有序数组：先把值复制到临时数组，再合并回去
>     *
>     * @param nums
>     * @param left
>     * @param mid   [left, mid] 有序，[mid + 1, right] 有序
>     * @param right
>     * @param temp  全局使用的临时数组
>     */
>    private void mergeOfTwoSortedArray(int[] nums, int left, int mid, int right, int[] temp) {
>        System.arraycopy(nums, left, temp, left, right + 1 - left);
>
>        int i = left;
>        int j = mid + 1;
>
>        for (int k = left; k <= right; k++) {
>            if (i == mid + 1) {
>                nums[k] = temp[j];
>                j++;
>            } else if (j == right + 1) {
>                nums[k] = temp[i];
>                i++;
>            } else if (temp[i] <= temp[j]) {
>                // 注意写成 < 就丢失了稳定性（相同元素原来靠前的排序以后依然靠前）
>                nums[k] = temp[i];
>                i++;
>            } else {
>                // temp[i] > temp[j]
>                nums[k] = temp[j];
>                j++;
>            }
>        }
>    }
>}
>```



## 选择排序

>每一轮选取未排定的部分中**最小**的部分交换到未排定部分的最开头，经过若干个步骤，就能排定整个数组。即：先选出最小的，再选出第 2 小的，以此类推。
>
>```java
>public class Solution {
>
>    // 选择排序：每一轮选择最小元素交换到未排定部分的开头
>
>    public int[] sortArray(int[] nums) {
>        int len = nums.length;
>        // 循环不变量：[0, i) 有序，且该区间里所有元素就是最终排定的样子
>        for (int i = 0; i < len - 1; i++) {
>            // 选择区间 [i, len - 1] 里最小的元素的索引，交换到下标 i
>            int minIndex = i;
>            for (int j = i + 1; j < len; j++) {
>                if (nums[j] < nums[minIndex]) {
>                    minIndex = j;
>                }
>            }
>            swap(nums, i, minIndex);
>        }
>        return nums;
>    }
>
>    private void swap(int[] nums, int index1, int index2) {
>        int temp = nums[index1];
>        nums[index1] = nums[index2];
>        nums[index2] = temp;
>    }
>
>    public static void main(String[] args) {
>        int[] nums = {5, 2, 3, 1};
>        Solution solution = new Solution();
>        int[] res = solution.sortArray(nums);
>        System.out.println(Arrays.toString(res));
>    }
>}
>```

## 插入排序

>每次将一个数字插入一个有序的数组里，成为一个长度更长的有序数组，有限次操作以后，数组整体有序。
>
>```java
>public class Solution {
>
>    // 插入排序：稳定排序，在接近有序的情况下，表现优异
>
>    public int[] sortArray(int[] nums) {
>        int len = nums.length;
>        // 循环不变量：将 nums[i] 插入到区间 [0, i) 使之成为有序数组
>        for (int i = 1; i < len; i++) {
>            // 先暂存这个元素，然后之前元素逐个后移，留出空位
>            int temp = nums[i];
>            int j = i;
>            // 注意边界 j > 0
>            while (j > 0 && nums[j - 1] > temp) {
>                nums[j] = nums[j - 1];
>                j--;
>            }
>            nums[j] = temp;
>        }
>        return nums;
>    }
>}
>
>```



## 冒泡排序

>- 基本思想：外层循环每一次经过两两比较，把每一轮未排定部分最大的元素放到了数组的末尾；
>- 「冒泡排序」有个特点：在遍历的过程中，提前检测到数组是有序的，从而结束排序，而不像「选择排序」那样，即使输入数据是有序的，「选择排序」依然需要「傻乎乎」地走完所有的流程。
>
>```java
>public class Solution {
>
>    // 冒泡排序：超时
>
>    public int[] sortArray(int[] nums) {
>        int len = nums.length;
>        for (int i = len - 1; i >= 0; i--) {
>            // 先默认数组是有序的，只要发生一次交换，就必须进行下一轮比较，
>            // 如果在内层循环中，都没有执行一次交换操作，说明此时数组已经是升序数组
>            boolean sorted = true;
>            for (int j = 0; j < i; j++) {
>                if (nums[j] > nums[j + 1]) {
>                    swap(nums, j, j + 1);
>                    sorted = false;
>                }
>            }
>            if (sorted) {
>                break;
>            }
>        }
>        return nums;
>    }
>
>    private void swap(int[] nums, int index1, int index2) {
>        int temp = nums[index1];
>        nums[index1] = nums[index2];
>        nums[index2] = temp;
>    }
>}
>```



## `Arrays.sort() TimSort`底层数据结构

>1.  插入排序< 双轴快排<归并排序  正常普通排序
>2. 如果是字符型数组或者short类型数组  当数组当读大于3200时候 那么计数排序优先于快速排序  这是因为字符或者short类型占用空间小

>```java
>/**
>* The maximum number of runs in merge sort.
>*/	
>private static final int MAX_RUN_COUNT = 67;			//如果数组长度大于286 在这里判断是不是具备结构 具备使用归并排序
>																					//判断具不具备结构  降序序列的个数如果大于67 采用快速排序 如果小67 归并排序
>/**
>* The maximum length of run in merge sort.
>*/
>private static final int MAX_RUN_LENGTH = 33;
>
>/**
>* 如果带排序的数组的长度小于286 那么快速排序优先于归并排序     	快速排序使用的是双轴快速排序
>*/
>private static final int QUICKSORT_THRESHOLD = 286;
>
>/**
>* 如果待排序数组长度小于47 插入排序优先于快速排序
>*/
>private static final int INSERTION_SORT_THRESHOLD = 47;
>
>/**
>* 如果待排序的 字节数组长度大于29 计数排序优先于插入排序
>*/
>private static final int COUNTING_SORT_THRESHOLD_FOR_BYTE = 29;
>
>/**
>* If the length of a short or char array to be sorted is greater
>* than this constant, counting sort is used in preference to Quicksort.
>* 如果时 short或者char类型数组长度大于3200 计数排序优先于快速排序
>*/
>private static final int COUNTING_SORT_THRESHOLD_FOR_SHORT_OR_CHAR = 3200;
>```
>
>- `67` 参数意义  在数组长度大于286的情况下 先判断具不具备结构  实际逻辑是分组排序，每个降序序列为一个组，像`1,9,8,7,6,8。9到6`是降序，为一个组，然后把降序的一组排成升序：`1,6,7,8,9,8`。然后再从最后的8开始继续往后面找。每遇到这样一个降序组，++count，当count大于`MAX_RUN_COUNT（67）`，被判断为这个数组不具备结构，也就是说这数据时而升时而降，波峰波谷太多，排列太过陡峭，说明不适合采用归并排序，还是使用快速排序为宜。
>- `47<=len<=286` 采用双轴快速排序
>- `len<=47`  采用插入排序  插入排序在数组长度较小的时候会快点 因为不用递归 分组
>- `len>=29`  字节数组长度若是大于29  采用计数排序 
>- `short[] byte[] len>=3200` 采用计数排序
>
>------------------------------------------------------------------
>
>- `Arrays.sort()`就是只能对基本类型的数组进行排序  基本类型无所谓稳定不稳定  采用  插入 快排(不稳定)  归并 计数  4种排序方案  
>- `TimSort`对象数据类型数组使用TimSort排序是因为（或者换句话说，对象数据类型不使用快排是因为）：
>- 对象数据类型要求稳定性，需要采用稳定的归并+二分查找插入排序。
>- 对于对象来说，比较操作相对耗时，所以用比较操作较少的归并排序可以扬长避短。





# ==TOP K 堆排序 快排==



## [最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

>思路： 先问面试官 数组中的数值有范围么。
>
>https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/      时间复杂度不会分析
>
>1. 如果数组中的值要是有范围的话并且还不算大 可以采用计数排序   时间复杂度O(N)  
>2. 建立大根堆 进行排序      时间复杂度O(nlogk)    空间复杂度O(k)
>3. 快速排序轴点==k-1        最好时间复杂度O(n)    最坏O(n^2)  



## [数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

>跟上边最小的K个数思路是一样的呢    
>
>1. `len-k` 这里边就是建造成正序  
>2. 快速排序找轴节点 正好等于 `len-k `   
>3. 维持K个最大堆呗  





## [前 K 个高频数组元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

>跟前K个高频单词处理模式差不多  但是这里边就是换成数字了呢 
>
>1. `HashMap` 来计数
>2. 重写`PriorityQueue`
>3. `if(minHeap.size()>k) minHeap.poll();`



## [前K个高频单词](https://leetcode-cn.com/problems/top-k-frequent-words/)

>```
>输入: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
>输出: ["i", "love"]       单词顺序相等的时候按照 单词排序为标准
>```
>
>1. 首先 建立一个`HashMap`  来添加元素 记录每个元素出现频率
>2. 建立一个最小堆 `PriorityQueue<String> minHeap=new PriorityQueue<String>((o1,o2)->{})`
>3. `for(String word : map.keySet)`
>
>----
>
>时间复杂度分析： https://leetcode-cn.com/problems/top-k-frequent-words/solution/qian-kge-gao-pin-dan-ci-by-leetcode-solu-3qk0/



## [根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

>```
>rett   输出 eert 或者 eetr
>```
>
>这个跟前K个高频单词处理模式差不多  
>
>1. `Hashmap` 来计数
>2. 重写`PriorityQueue`



## [最接近原点的 K 个点](https://leetcode-cn.com/problems/k-closest-points-to-origin/)

>二维数组 在这里就是最接近原点
>
>
>
>

## [把数组组合排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

>```
>输入: [10,2]
>输出: "102"
>```
>
>1. 还是要利用堆的思想呗  在这里哈呢 
>2. 把数字转化成`String`类型 
>3. `PriorityQueue<String> ((01,02)-> return o1+o2 .compareTo(o2+o1)`



# ==归并排序==

## [数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

>```xml
>在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。
>
>输入: [7,5,6,4]
>输出: 5
>```
>
>思路：
>
>1. 双重`for` 循环指定不是最优解  O(n^2)  
>2. 使用归并排序  在合并的时候做判断 时间复杂度O(nlogn) 空间复杂度O(n) 





## [数组单调和](https://www.nowcoder.com/questionTerminal/8397609ba7054da382c4599d42e494f3)

>```xml
>现定义数组单调和为所有元素i的f(i)值之和。这里的f(i)函数定义为元素i左边(不包括其自身)小于等于它的数字之和。请设计一个高效算法，计算数组的单调和。
>给定一个数组A同时给定数组的大小n，请返回数组的单调和。保证数组大小小于等于500，同时保证单调和不会超过int范围。
>
>[1,3,5,2,4,6],6
>返回：27
>```
>
>1. 如果就是走两遍循环就是可以呢  O(n^2)  
>2. 但是我们就是可以使用归并排序  时间复杂度O(nlogn) 利用归并排序的归 之后在这里进行计算数组单调和





## [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)



## [至少有 K 个重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/)

>不会 这个题 至少有K个重复的字符串  



## [ 数组的相对排序](https://leetcode-cn.com/problems/relative-sort-array/)

>```xml
>输入：arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
>输出：[2,2,2,1,4,3,3,9,6,7,19]
>```
>
>1. 这种其他做法并不怎么好做呢 所以利用空间来换时间呗  
>2. 利用桶排序  不知道跟计数排序有什么区别  再说吧



## [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

>这里边也算是排序 合并区间这个样子呢。 其实也算是双指针进行排序呗 在这里哈呢



# ==---------------------------------------------------------------数组==



# ==Bitmap位图==

>用这种位图做起来就是比较好

## 1~100 万中数组缺失、或者重复的数字

>```java
>import java.util.ArrayList;
>import java.util.Arrays;
>import java.util.List;
>
>public class BitMap {
>    /**
>     * 如何确定用来存放数据的位图数组bitmap的大小？以及每个数据在bitmap中的位置？
>     * 如何对一个int类型的32为bit的某一个bit进行赋值操作？
>     * 如何对一个int类型的32为bit的某一个bit进行读取操作？
>     * 如何判重？
>     * 如何根据bitmap恢复原始数据？
>     */
>    private int[] bitmap;
>    public BitMap(int maxValue) {
>        int size = maxValue / 32 + 1;       //  bitmap 数组大小呗
>        bitmap = new int[size];
>        this.maxValue = maxValue;
>    }
>    public List<Integer> repeatNumList = new ArrayList<>();
>    public List<Integer> noExistNumList = new ArrayList<>();
>    private int maxValue;
>
>    //添加元素 并判断是否重复呗 在这里哈呢
>    public void add(int[] nums) {
>        for (int i = 0; i < nums.length; i++) {
>            int value = nums[i];
>            int index = value / 32;             //元素位于数组下标位置
>            int offset = value % 32 - 1;        //一个 int类型就是四个字节 32位二进制
>            int temp = bitmap[index];
>            bitmap[index] = bitmap[index] | 1 << offset;  //1<<offset即为value的bitmap的位置，与目前有的值进行或操作进行合并
>            if (temp == bitmap[index]) {
>                //这里边就是代表重复了  因为如果先前为0 现在为1 不会重复  如果先前就是为1 现在也为1 在这里就是重复了呢
>                repeatNumList.add(value);
>            }
>        }
>    }
>    public List<Integer> getRepeatNumList() {
>        return repeatNumList;
>    }
>    //遍历寻找 确实的元素呗  找出不存在的元素
>    public List<Integer> findLoseNum() {
>        int len = bitmap.length;
>        for (int i = 0; i < len; i++) {
>            //一个 int 类型就是32个字节
>            int num = bitmap[i];
>            for (int j = 0; j < 32; j++) {
>                boolean isExist = ((num >> j) & 0x01) == 0x01;    //如果为1 就是代表当前元素存在
>                if (!isExist) {
>                    //找到那个缺失的数字呗
>                    int loss = i * 32 + j + 1;
>                    if (loss < maxValue) {
>                        noExistNumList.add(loss);
>                    }
>                }
>            }
>        }
>        return noExistNumList;
>    }
>
>    public static void main(String[] args) {
>        BitMap whig = new BitMap(100);  // 找 1到100之中重复的数字 和 不存在的数字
>        int[] nums = {1, 1, 3, 4, 6, 7, 8, 9, 22, 44, 55, 99, 100, 100};
>        whig.add(nums);
>        System.out.println(whig.getRepeatNumList());
>        System.out.println(whig.findLoseNum());
>    }
>}
>```





## 学生成绩排序

>注意这里边学生成绩排序：
>
>主要点 就是成绩是有范围的 我们就是可以使用技术排序呢



## [比特位计数](https://leetcode-cn.com/problems/counting-bits/)

>计算二进制中1的个数 在这里哈呢
>
>关键点就是解释清楚好 `res[i]==res[i&i-1]+1` 这个公式的由来呗   



## [ 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)





# ==寻找中位数、众数、多数元素、交集==

## [数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

>```xml
>[2,3,4] 的中位数是 3
>[2,3]   的中位数是 (2 + 3) / 2 = 2.5
>```
>
>思路：
>
>1. 建立两个堆  一个是大顶堆 一个是小顶堆
>2. 小顶堆存放大的元素  大顶堆存放小的元素 
>3. 在添加元素的时候 `A.add(B.poll)` 先让相反的进行添加元素呢



## [寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

>```xml
>输入：nums1 = [1,2], nums2 = [3,4]
>输出：2.50000
>解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
>```
>
>1. 要求时间复杂度O(log(m+n))    所以在这里边指定就是二分查找呢 
>
>https://leetcode-cn.com/problems/median-of-two-sorted-arrays/comments/

## [多数元素](https://leetcode-cn.com/problems/majority-element/)

>摩尔投票法
>
>【笔记】摩尔投票法。该算法用于1/2情况，它说：“在任何数组中，出现次数大于该数组长度一半的值只能有一个。”

## [求众数 II](https://leetcode-cn.com/problems/majority-element-ii/)

>给定一个大小为 *n* 的整数数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。
>
>摩尔投票法。该算法用于1/2情况，它说：“在任何数组中，出现次数大于该数组长度一半的值只能有一个。”
>
>那么，改进一下用于1/3。可以着么说：“在任何数组中，出现次数大于该数组长度1/3的值最多只有两个。”
>
>于是，需要定义两个变量。空间复杂度为O(1)。





## [两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

>https://blog.csdn.net/sinat_20177327/article/details/80100081
>
>不管是有序还是无序： 可以采用两个set集合来做
>
>-----
>
>如果是有序的：
>
>1. hashset来做
>2. 双指针 O(m+n)
>3. 遍历其中一个数组 对另一个数组进行二分



# ==循环不变量==

## [颜色分类](https://leetcode-cn.com/problems/sort-colors/)

>```xml
>输入：nums = [2,0,2,1,1,0]
>输出：[0,0,1,1,2,2]
>```
>
>思路：
>
>1. 可以循环遍历两次 时间复杂度依然是O(N)
>2. 设置两个循环不变量  `zero=0  two=len-1` 双指针进行遍历  
>3. 直接进行快速排序  时间复杂度O(nlogn) 



## [ 移动零](https://leetcode-cn.com/problems/move-zeroes/)

>```xml
>输入: [0,1,0,3,12]
>输出: [1,3,12,0,0]   这里边就是一定要保持元素相对顺序呢 
>```
>
>难点： 这里边0也是要保持相对顺序呢  在这里哈呢   其他元素也是要保持相对顺序
>
>1. 正常思路： 遇到0 往后边元素进行叫唤  但是这种就是存在打破原来顺序 不可取
>2. `left 表示数组中为0的第一个位置`  直接对`right`进行循环遍历呗 



## [移除元素](https://leetcode-cn.com/problems/remove-element/)

>移动零 和 这里移除元素 差不多都是一样的 
>
>1. 定义一个循环不变量  进行反向思维 找不是特定元素的其他元素呗 
>2. `left=0` 表示为待删除元素的起始位置
>
>```java
>        int left=0;              		//在这里Left 表示为val的起始位置  
>        int right=0;
>        while(right<=len-1){
>            if(nums[right]!=val){		//这里边要写成nums[right]!=val  不一定要写成nums[right]==val
>                if(left!=right)swap(nums,right,left);
>                left++;
>            }
>            right++;
>        }
>```



## [删除有序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

>```
>输入：nums = [0,0,1,1,1,2,2,3,3,4]
>输出：5, nums = [0,1,2,3,4]
>```
>
>1. 确定`left=1`  表示不重复元素的起始位置呢  
>2. `if(nums[right]!=pre)` 当前元素跟前边元素不相等的时候 我们就是置换一下`left right` 元素呢







# ==二维数组遍历==

## [对角线遍历](https://leetcode-cn.com/problems/diagonal-traverse/)

>```xml
>输入:
>[
> [ 1, 2, 3 ],
> [ 4, 5, 6 ],
> [ 7, 8, 9 ]
>]
>输出:  [1,2,4,7,5,3,6,8,9]
>```
>
>1. 根据题目描述 我们要观察遍历方式
>2. `col + row` 为偶数我们就是向上遍历  为奇数我们就是向下遍历



## [螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

>螺旋矩阵 在这里就是顺时针打印矩阵呗 
>
>1. 定义四个变量
>2. `while(count<=n*m)` 根据元素个数来维持



## [螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

>顺时针填充矩阵中的个数被
>
>1. 原理都是一样 定义四个变量
>2. `while(num <=n*n)`





## [旋转矩阵90](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

>将矩阵元素进行90度旋转呗
>
>1. 先对角线对称一下 在原地对称就可以
>2. 在以竖轴中心进行对称



## [二维有序矩阵中第 K 小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)

><img src="https://assets.leetcode-cn.com/solution-static/378/378_fig3.png" alt="fig3" style="zoom:30%;" />
>
>首先是找第K小的元素
>
>思路： 直接就是排序没有用到上述二维矩阵的性质  
>
>可以利用二分查找 例如上图所示
>
>1. 首先初始化最小值 和 最大值 分别是两个对角线点
>2. 利用`l=mid+1  r=mid count&&k 判断`
>
>```java
>   public int kthSmallest(int[][] matrix, int k) {
>        int l = matrix[0][0];
>        int r = matrix[matrix.length-1][matrix.length-1];
>        int mid;
>        while(l < r) {
>            mid = (l + r) >> 1;
>            int cnt=count(matrix,mid);
>            if(cnt>=k) r=mid;
>            }
>            else {
>                l = mid + 1;
>            }
>        }
>        return l;
>    }
>    // 快速计算矩阵中<=num的个数，O(n)
>    private int count(int[][] m, int num) {
>        int i = 0;
>        int j = m.length-1;
>        int cnt = 0;
>        while(i < m.length && j >= 0) {
>            if(m[i][j] > num) {
>                j--;
>            } 
>            else {
>                cnt += j + 1;
>                i++;
>            }
>        }
>        return cnt;
>    }
>```
>
>**解释 l 为什么最后一定在矩阵当中。**
>
>```xml
>可以肯定的是在二分搜索过程中，我们一定会找到一个mid，使得count(matrix,mid)=k，即matrix中<=mid的数量为k的一个mid值，设matrix中的第k小的元素为mk，此时这个mid满足mid>=mk，并且在这次搜索我们会使r==mid。
>
>从这以后，如果再次求得的mid满足mk<=mid<=r，我们都会更新r为mid，也就是说r一定满足r>=mk。
>
>我们再来看l，只有当mid<mk时，才会执行l=mid+1，也就是说必定有l<=mk。 循环终止的条件为l>=r，而我们又知道l<=mk&&r>=mk，当且仅当l==r==mk时，循环退出，所以最终的l一定时矩阵中的第k小的数mk。
>```



## [搜索有序二维矩阵-字节二面](https://leetcode-cn.com/problems/search-a-2d-matrix/)

>时间复杂度： 最坏情况 重最右边走到最下边 重最下边走到最左边  所以O(m+n) 



## [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

>时间复杂度度 O(nlogn)  在这里主要就是排序算法的涉及呗  
>
>二维数组： 排序规则就是根据数组
>
>一定要注意当前`right 可能比右边right也大` 并且可能一直在循环下去 所以要用`while`循环



# ==数组中出现重复、一次、丢失 异或的数字==

>这个使用技巧就是有点多呢哈  一定就是要想到异或这个重要点呗

## [数组中重复的数据](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

> ```
> [4,3,2,7,8,2,3,1]
> [2,3]
> ```
>
> 这里边数据重复： 题目中有限制范围就是 `1<=a[i]<=n`   并且要求空间复杂度为O(1)。
>
> 两种思路：
>
> ```java
>     public List<Integer> findDuplicates(int[] nums) {
>         int len=nums.length;
>         List<Integer> list=new ArrayList<>();
> 
>         for(int i=0; i<len; i++){
>             int index = Math.abs(nums[i]);
>             if(nums[index-1]>0){
>                 nums[index-1]*=-1;
>             }
>             else{
>                 list.add(index);
>             }
>         }
>         return list;
>     }
> ```
>
> 思路： 就是当前值对应数组的下标  之后变成负数 再次判断的时候如果在这里还是为负数 那么就是直接加入返回值呢



## [数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

>```
>[2, 3, 1, 0, 2, 5, 3]
>输出：2 或 3 
>```
>
>在这里不能使用上边方法 就是数组范围是在`0<=a[i]<=n-1` 并且在这里数组也不知道重复了几次 。返回值在这里并没有要找到全部数字。找到单独的在这里就是可以呢。
>
>思路1：
>
>1.  在这里就是直接进行数组下标进行对换 
>2. 使用`while`循环 如果就是相等 `index++`  
>3. 不相等找对应数组下标直到相等
>
>-------
>
>上述是对数组中重复的数字找出来一个就行  增加难度 在这里我们就是找出所有重复的数字 不管重复了几次呢
>
>```java
>    public static List<Integer> find(int[] nums) {
>        int len = nums.length;
>        List<Integer> list = new ArrayList<>();
>
>        for (int i = 0; i < nums.length; i++) {
>            int index = nums[i];
>            nums[(index % len)] = nums[index%len] + len;
>        }
>        for (int i = 0; i < len; i++) {
>            if (nums[i] > 2 * len) list.add(i);     //这里边也是精髓啊  list.add(i) 即使原来的数组
>        }
>        return list;
>    }
>```
>
>是根据数组中重复的数据是一个思路
>
>1. 在原数组上进行+len
>2. `index%len`  两边都要取呢 否则这里就是会造成数组越界异常呗
>3. 在一次循环进行判断`nums[i]>2*len`  并且添加的时候也是利用到数组下标  因为原数据已经就是进行改动了呗 在这里哈呢`list.add(i)` 重点



## [只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

>```
>输入: [4,1,2,1,2]
>输出: 4
>```
>
>思路：异或 `^` 这个关键点就是一定要想到呢 
>
>一次循环遍历来进行异或操作  最终找到只出现一次的数字呗



## [只出现一次的数字 III](https://leetcode-cn.com/problems/single-number-iii/)

>```
>输入：nums = [1,2,1,3,2,5]
>输出：[3,5]
>解释：[5, 3] 也是有效的答案。
>```
>
>对比上边这个就是增加难度呗  找出所有只出现一次的数字呢
>
>如果面试当中没有要求是否是常数级空间来做这件事。 我们就是可以使用`hashmap`来存储 之后找到所有`value==1`的情况呗。
>
>思路：
>
>1. 对所有值进行异或 异或结果是两个不一样的数字的异或结果
>2. 对结果进行二进制查找为`1`的标志位  代表这两个数字是不一样的进行区别  
>3. 利用区分出来的`div` 再次对数组进行一次遍历 也是对应将数组分成两组 最后找到两个不想同的数字呗



## [丢失的数字](https://leetcode-cn.com/problems/missing-number/)

>```xml
>给定一个包含 [0, n] 中 n 个数的数组 nums ，找出 [0, n]这个范围内没有出现在数组中的那个数。
>
>输入：nums = [3,0,1]
>输出：2
>解释：n = 3，因为有 3 个数字，所以所有的数字都在范围 [0,3] 内。2 是丢失的数字，因为它没有出现在 nums 中。
>```
>
>两种思路： 要求时间复杂度为O(n) 并且要求你不能使用额外的空间呢
>
>思路1：
>
>1. 遍历数组同时 `res=nums.length  res=res^nums[i]^i`
>
>思路2：
>
>1. 遍历数组同时`sum=0;  sum=sum+nums[i]-i` 





## [丢失的数据II](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

>跟上题形式是差不多的。但是在这里就是需要找到所有丢失的数据呗。
>
>```
>输入：nums = [4,3,2,7,8,2,3,1]   //nums[i] 在这里是在区间1-n呢 
>输出：[5,6]
>```
>
>思路：
>
>1. 不管重不重复 我们就是把当前元素作为数组下标找到对应元素使其为负数
>2. 再次遍历的时候 如果为正数 我们就是添加对应的下标。`list.add(i+1)`



## [缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

>```
>输入：nums = [3,4,-1,1]
>输出：2
>```
>
>这个题就是比较难 在这里哈呢  在这里还是需要进行不停的交换呗 



# ==数组子序列问题->DP==



## 数组中左边最大、右边最小的元素

>```
>//输入：[2, 3, 1, 8, 9, 20, 12]
>//输出：3, 4
>//解释：数组中 8, 9 满足题目要求，他们的索引分别是 3、4
>```
>
>思路： 1. 要求时间复杂度 O(N)  我们在这里就是该怎么办呗 
>
>  		 2. 就是再新建立两个数组 一个表示当前元素左边最大值  一个表示当前元素右边最大值呗
>  	 	 3. 这种做法就是典型的时间换取空间被  
>
>```java
> public static List<Integer> find(int[] nums) {
>       //找到左边数字比较当前数字小 右边数字比当前数字大的两个数组呗
>       //这种就是进行时间上的优化 我们就是可以使用空间进行优化呗 在这里哈呢
>       int len = nums.length;
>       int[] left_max = new int[len];          //[0,i)     最大的      并且在这里边数组需要初始值 最小值呢
>       int[] right_min = new int[len];         //(i,len-1] 中最下的    在这里数组需要初始值最大值呢 在这里哈呢
>       Arrays.fill(left_max, Integer.MIN_VALUE);
>       Arrays.fill(right_min, Integer.MAX_VALUE);
>       for (int i = 1; i < len; i++) {
>           left_max[i] = Math.max(left_max[i - 1], nums[i - 1]);
>       }
>       for (int i = len - 2; i >= 0; i--) {
>           right_min[i] = Math.min(nums[i + 1], right_min[i + 1]);  //后续遍历 在这里我们找到右边最小值呗
>       }
>       List<Integer> list = new ArrayList<>();
>       for (int i = 0; i < len; i++) {
>           if (left_max[i] < nums[i] && nums[i] < right_min[i]) {
>               list.add(i);
>           }
>       }
>       return list;
>   }
>```



## [最短无序连续子数组](https://leetcode-cn.com/problems/shortest-unsorted-continuous-subarray/)

>```xml
>输入：nums = [2,6,4,8,10,9,15]
>输出：5
>解释：你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
>```
>
>双指针进行一次遍历：
>
>在双指针系列还存在这个东东





## [数组最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

>```
>输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
>输出：6
>解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
>```
>
>```java
>dp[i]  == dp[i-1]+nums[i] (dp[i]>0)    nums[i] (dp[i]<0) 在这里就是两种呗
>```
>
>```java
>dp[i]= (dp[i-1]<0)? nums[i]:dp[i-1]+nums[i];  
>res=Math.max(res,dp[i]);      这里边就是可以利用dp 来做呗  对巴哈呢
>```





## [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

>```
>输入: [2,3,-2,4]
>输出: 6
>解释: 子数组 [2,3] 有最大乘积 6。
>```
>
>思路： 差不多也是采用动态规划 但是在这里两个变量就是可以维持一下呗
>
>1. 遍历数组时，记录当前最大值 并不断更新
>2. 我们就是需要维持两个变量  一个是最大值 一个是最下值
>3. 当遇到负数的时候 最大值和最小值进行交换  
>4. 并且维持一个变量  在遍历的时候就是更新当前连续子数组最大值呗



## [最长重复子数组](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/)

>```
>输入：
>A: [1,2,3,2,1]
>B: [3,2,1,4,7]
>输出：3
>长度最长的公共子数组是 [3, 2, 1] 。
>```
>
>思路：
>
>```xml
>1.dp[i][j] 表示以i为结尾的A数组 和以j为结尾的B数组 的最长重复数组
>2.dp[i][j]--->  if(nums[i]==nums[j]) dp[i][j]=dp[i-1][j-1]+1;    else{dp[i][j]==0}
>3.由于这里边用到 dp[i-1][j-1] 所以我们需要就是初始化长度需要大一些
>```
>
>----
>
>时间复杂度:   O(n^2)
>
>空间复杂度：O(1)





## [最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

>```
>输入：text1 = "abcde", text2 = "ace" 
>输出：3  
>解释：最长公共子序列是 "ace" ，它的长度为 3 。
>```
>
>思路：
>
>```xml
>1.这里边最长公共子序列 就是最长公共子数组是不一样的 最长子数组是连续的 在这里不是连续的呢
>2.dp[i][j] 表示以i 为结尾txt1 和以 J为结果txt2 的最长公共子序列呗    因为这里边就是需要dp[i-1][j-1] 所以初始化长度大一
>		3.if(nums[i-1]==nums[j-1]) dp[i][j]=dp[i-1][j-1]+1
>		  else 										 dp[i][j]=Math.max(dp[i-1][j],dp[i][j-1]);
>```
>
>----
>
>时间复杂度： O(N^2)
>
>空间复杂度:   O(1)



## [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

>```
>输入：nums = [10,9,2,5,3,7,101,18]
>解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。
>```
>
>思路：
>
>```xml
>dp[i] 表示以 nums[i] 结尾的最长上升子序列的长度。即：在 [0, .., i] 的范围内，选择以数字 nums[i] 结尾可以获得的最长上升子序列的长度。
>
>遍历到 nums[i] 的时候，我们应该把下标区间 [0, ... ,i - 1] 的 dp 值都看一遍，如果当前的数 nums[i] 大于之前的某个数，那么 nums[i] 就可以接在这个数后面形成一个更长的上升子序列。把前边dp[i]中最大的拿出来进行+1 操作 
>
>并且dp初始值 一定要全赋值为1呢 在这里哈呢 
>for (int i = 1; i < len; i++) {
>       for (int j = 0; j < i; j++) {
>           if (nums[j] < nums[i]) {
>               dp[i] = Math.max(dp[j] + 1, dp[i]);
>           }
>       }
>}                                 
>```
>
>-----
>
>时间复杂度：O(N^2)
>
>空间复杂度：O(n^2)



## [最长连续递增序列](https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/)

>```xml
>输入：nums = [1,3,5,4,7]
>输出：3
>解释：最长连续递增序列是 [1,3,5], 长度为3。
>```
>
>思路：
>
>```xml
>这种跟最长递增序列是不一样呢。。 因为这里边可以进行连续操作呢  所以不用找[0...i]中最大的递增子序列 只需要往下排动就是可以了呢
>Arrays.fill(dp,1);
>1. if(nums[i]>nums[i-1]) dp[i]=dp[i-1]+1   更新res最大值
>```
>
>-----
>
>时间复杂度：O(N)
>
>空间复杂度：O(N)
>
>-------
>
>思路2：
>
>```xml
>可以不用试动态规划 只需要用一个count来维持记录就是可以呢
>           if(nums[i]>nums[i-1]){
>               count++;
>               res=Math.max(res,count);
>           }
>           else{
>               count=1;
>           }
>```

# ==N数之和、加、减==

>上述就是都要有一个前提条件： 就是相加或者相减不会出现溢出现象
>
>否则在这里我们就是要判断一下 是否用Long来接受呢
>
>

## [两数之和 -------hash](https://leetcode-cn.com/problems/two-sum/)

>leetcode第一题  这里边两数之和  
>
>如果进行排序  在双指针时间复杂度O(nlogn)
>
>经典的数组 在这里就是使用map来做呢

## [两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

> 直接进行双指针就可以呢  在这里哈呢

## [两数之和 IV - 输入 二叉树](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/)

>这里边是二叉树的形式  所以在这里我们就是使用

## [最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)

>字节面试题：
>
>```
>输入：nums = [-1,2,1,-4], target = 1
>输出：2
>解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
>```
>
>1. 思路：首先是进行排序
>2. `for 循环定位一个数字  之后进行双指针 比较一下`
>
>-----
>
>时间复杂度：O(N^2) 
>
>空间复杂度:   O(1)

## [三数之和](https://leetcode-cn.com/problems/3sum/)

>```
>输入：nums = [-1,0,1,2,-1,-4]
>输出：[[-1,-1,2],[-1,0,1]]
>```
>
>这里边输出的答案就是不带有重复元素呢   在这里如果要使用`map` 来做就是非常困难
>
>1. 排序
>2. 定位一个元素  之后进行双指针
>3. 时间复杂度O(n^2)

## [四数之和](https://leetcode-cn.com/problems/4sum/)

>```
>输入：nums = [1,0,-1,0,-2,2], target = 0
>输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
>```
>
>也是双指针做法 时间复杂度O(n^3)



## [四数相加 II-------hash](https://leetcode-cn.com/problems/4sum-ii/)

>```xml
>A = [ 1, 2]
>B = [-2,-1]
>C = [-1, 2]
>D = [ 0, 2]
>A+B+C+D==0  寻找合适的元素呗  在这里哈呢
>```
>
>1. 四个数组 没有排序  而且双指针在这里好像作用效果并不是很大 
>2. 定位两个数组  使用`hashmap`  时间复杂度O(n^2)



## [三个数的最大乘积](https://leetcode-cn.com/problems/maximum-product-of-three-numbers/)

>```
>输入：nums = [1,2,3,4]
>输出：24
>```
>
>分析一下：
>
>1. 如果是全正数 或者就是 全负数  那么就是三个数最大的乘机
>2. 如果有正有负  那么就是两个最小的跟一个最大的   以及三个最大的 两个做对比
>
>----
>
>思路： 排序  O(nlog)
>
>​            重点： 五个变量 来遍历寻找三个最大的 和两个最小的



## [两个数组中的最小差](https://leetcode-cn.com/problems/smallest-difference-lcci/)

>还是双指针的做法  并判断是否有溢出现象呢 在这里哈呢







# ==排列 或者 排序、奇偶、合并==



## [下一个排列](https://leetcode-cn.com/problems/next-permutation/)

>```
>输入：nums = [1,2,3]
>输出：[1,3,2]          
>```
>
>思路：三步走 如果不走第2不 那么就是直接走第三步合并都是一样的  第三步使用双指针进行排序减少时间复杂度
>
>```xml
>1. 首先从后向前查找第一个顺序对 (i,i+1)，满足 a[i] < a[i+1]。这样「较小数」即为 a[i]。此时 [i+1,n) 必然是下降序列。
>
>2. 如果找到了顺序对，那么在区间 [i+1,n) 中从后向前查找第一个元素 j 满足 a[i] < a[j]。这样「较大数」即为 a[j]。
>
>3. 交换 a[i]与 a[j]，此时可以证明区间 [i+1,n) 必为降序。我们可以直接使用双指针反转区间 [i+1,n) 使其变为升序，而无需对该区间进行排序。
>```
>
>-----
>
>1. 时间复杂度：O(N) 只需要两趟扫描和一次反转  这种题在这里就是找规律 就是不能使用全排列的方法
>2. 空间复杂度：只需要常数的空间存放若干变量。



## [部分排序寻找起始索引和终止索引](https://leetcode-cn.com/problems/sub-sort-lcci/)

>```
>输入： [1,2,4,7,10,11,7,12,6,7,16,18,19]
>输出： [3,9]
>```
>
>在这里就是找出 部分无序的起始索引和终止索引呗  
>
>1. 可以建立一个新数组 进行比较 判断一下
>2. 思路二 双指针前后进行遍历 更新乱序索引下表  这个一次遍历比较牛逼







## 数组中左边最大、右边最小的元素

>```
>//输入：[2, 3, 1, 8, 9, 20, 12]
>//输出：3, 4
>//解释：数组中 8, 9 满足题目要求，他们的索引分别是 3、4
>```
>
>思路： 1. 要求时间复杂度 O(N)  我们在这里就是该怎么办呗 
>
> 		 2. 就是再新建立两个数组 一个表示当前元素左边最大值  一个表示当前元素右边最大值呗
> 	 	 3. 这种做法就是典型的时间换取空间被  
>
>```java
>public static List<Integer> find(int[] nums) {
>      //找到左边数字比较当前数字小 右边数字比当前数字大的两个数组呗
>      //这种就是进行时间上的优化 我们就是可以使用空间进行优化呗 在这里哈呢
>      int len = nums.length;
>      int[] left_max = new int[len];          //[0,i)     最大的      并且在这里边数组需要初始值 最小值呢
>      int[] right_min = new int[len];         //(i,len-1] 中最下的    在这里数组需要初始值最大值呢 在这里哈呢
>      Arrays.fill(left_max, Integer.MIN_VALUE);
>      Arrays.fill(right_min, Integer.MAX_VALUE);
>      for (int i = 1; i < len; i++) {
>          left_max[i] = Math.max(left_max[i - 1], nums[i - 1]);
>      }
>      for (int i = len - 2; i >= 0; i--) {
>          right_min[i] = Math.min(nums[i + 1], right_min[i + 1]);  //后续遍历 在这里我们找到右边最小值呗
>      }
>      List<Integer> list = new ArrayList<>();
>      for (int i = 0; i < len; i++) {
>          if (left_max[i] < nums[i] && nums[i] < right_min[i]) {
>              list.add(i);
>          }
>      }
>      return list;
>  }
>```

## [调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

>思路差不多呢 在这里哈呢
>
>就是双指针进行判断
>
>1. `left` 如果还是奇数 就是做++操作
>2. `right` 如果还是偶数就--操作
>3. 如果上述不满足 交换`left 和 right`



## 偶数排在奇数前边 并保持相对顺序

>如果不保持相对顺序  就是双指针前后进行叫唤就是可以呢
>
>保持相对顺序：  利用一个集合
>
>1. 先遍历一遍  添加偶数
>2. 在遍历一遍 添加奇数
>
>时间复杂度：o(2n)
>
>空间复杂度：o(n)





## [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

## [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

>```xml
>输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
>输出：[1,2,2,3,5,6]
>```
>
>1. 如果新建立一个数组 双指针重前向后排序的话  时间复杂度:O(m+n)   空间复杂度O(n)
>2. 题目给的挺有意思：第一个数组空间够  所以双指针重后边进行排序 排完序判断第二个数组还要剩余元素没  第一个数组就是本身了。时间复杂度O(m+n)  空间复杂度O(1)

## [移动零](https://leetcode-cn.com/problems/move-zeroes/)

>```
>输入: [0,1,0,3,12]
>输出: [1,3,12,0,0]
>给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
>```
>
>思路：
>
>1. 这里边双指针 定义一个`Left `表示开始0的下标元素
>2. 定义一个`right`当遇到不是0的元素就是跟`left`进行叫唤

## [颜色分类](https://leetcode-cn.com/problems/sort-colors/)

>这个跟上述差不多  就是循环不变量。





# ==---------------------------------------------------------------双指针==



>首先不要进入思维误区 ： 
>
>1. 双指针未必就是 `left==0 right=len-1` 也有空能双指针是`left==0 right==0`   例如[移动零](https://leetcode-cn.com/problems/move-zeroes/)

## [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)



## [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

>1. 双重for循环
>2. 动态规划
>3. 栈
>4. 双指针

# ==------------------------------------------------------------滑动窗口==



## [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)



## [替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

>```xml
>输入：s = "AABABBA", k = 1
>输出：4
>解释：
>将中间的一个'A'替换为'B',字符串变为 "AABBBBA"。
>子串 "BBBB" 有最长重复字母, 答案为 4。
>```
>
>典型的滑动窗口题  就是利用K的性质呗做运算



## [长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

>```xml
>输入：target = 7, nums = [2,3,1,2,4,3]
>输出：2
>解释：子数组 [4,3] 是该条件下的长度最小的子数组。
>```
>
>典型的滑动窗口：  
>
>但是要记录变量的时候一定就是要小心初始值 





## [找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

>1. 给定的数据范围有限，我们就是尽量使用`int[]`数组来计数呗，不要使用`HashMap`来计数呢，成本有点高
>2. 这种就是类似于计数排序   而且这个`while`条件就是很精彩呗 在这里哈呢



## [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

>1. 4.15在做一遍 没有做出来 
>2. 用双端队列存储数组下标 感觉就是有点诡异呢 在这里



## [滑动窗口中位数](https://leetcode-cn.com/problems/sliding-window-median/)

>1. 思路1： 利用数据流中的中位数这个题作为思路，自己设计数据结构，但是需要进行移除元素，保持窗口大小，有点难度
>2. 思路2： 利用`List` 插入二分排序，删除二分删除 返回值利用数组下标奇偶行来判断  不错的想法 应该重暴力法过来-->再想到这个办法



## [字符串的排列](https://leetcode-cn.com/problems/permutation-in-string/)



## [串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)

## [替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)



# ==----------------------------------------------------------------二分==

https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/

https://www.liwei.party/2019/06/17/leetcode-solution-new/search-insert-position/

>二分查找时间复杂度O(nlog(n))   
>
>符合题型：数组有序
>
>题型1：寻找目标值 target		**while(left<=right)**
>
>题型2：寻找目标值边界		    **while(left<=right)**
>
>题型3：寻找最大值和最小值 	**while(left<right)** 	使用排除法
>
>
>
>
>题型1：寻找目标值 target是常见题	这种我们就是寻找某一个特定的值 不用排除法来做
>
>```java
>class Solution{
>public int findTarget(int[] nums,int target){
>int len=target.length;
>int left=0. right=len-1;
>int mid=0;
>while(left<=right){		//这种最后就是数组元素都遍历了一遍 <=呢 在这里哈呢
>mid=left+(right-left)/2;
>if(nums[mid]==target)
> return mid;
>if(nums[mid]>target)
> right=mid-1;
>else
> left=mid+1;
>}
>return -1;
>}
>}
>```
>
>
>
>题型2：数组中存在重复元素  寻找左右边界这种类型   nums={1,2,2,2,5} target=2;
>
>```java
>class Solution{	
>public int leftBound(int[] nums.int target){	//在这里就是寻找左边界
>int len=nums.length;
>int left=0,right=len-1,mid=0;
>while(left<=right){
>mid=left+(right-left)/2;
>if(nums[mid]==target)
> right=mid-1;
>else if(nums[mid]>target)
> right=mid-1;
>else if(nums[mid]<target)
> left=mid+1;
>}
>// 我们在这里就是要寻找左边界呢 在这里继续进行一下判断被 在这里哈呢
>if(left>=len || nums[left]!=target)
>return -1;
>return left;
>}
>}
>```
>
>- 寻找右边界呢  相等的时候 left=mid+1;
>
>```java
>class Solution{
> public int rightBound(int[] nums,int target){
>     int len=nums.length;
>     int left=0,right=len-1;
>     int mid=0;
>     while(left<=right){
>         if(nums[mid]==target)
>             left=mid+1;
>         else if(nums[mid]>target)
>             right=mid-1;
>         else if(nums[mid]<target)
>             left=mid+1;
>     }
>     //判断一下右边界是否是小于0 
>     if(nums[right]!=target && right<0)
>         return -1;
>     return right;
> }
>}
>```
>
>
>
>题型3：寻找最大值和最小值		 **在循环体内部排除元素（在解决复杂问题时非常有用) **
>
>退出循环的时候 left 和 right 重合，区间 [left, right] 只剩下成 1 个元素，这个元素 有可能 就是我们要找的元素。可以归纳为「左右边界向中间走，两边夹」，这种思路在解决复杂问题的时候，可以使得思考的过程变得简单。
>
>
>
>
>```java
>public class Solution{
> public int MaxOrMinFindTarget(int[] nums){
>     int len=nums.length;
>     int left=0,right=len-1,mid=0;
>     while(left<right){
>         //这里边我们就是习惯于向下取整呗  	
>         mid=left+(right-left)/2;
>
>         if(check(mid))
>             left=mid+1;   // 下一轮搜索区间是 [mid + 1, right]
>         else
>             right=mid;	  // 下一轮搜索区间是 [left, mid]
>        } 
>     }
>	     // 退出循环的时候，程序只剩下一个元素没有看到，视情况，是否需要单独判断 left（或者 right）这个下标的元素是否符合题意
> 	return nums[left||right||mid] //退出循环的时候	left==right
> }
>}
>```



## [二维有序矩阵中第 K 小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)

>这里边就是简单利用到二分查找 。  二分查找就是在这里利用数组的有序性 时间复杂度





## [x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

>输入4返回2   输入8也返回2
>
>使用二分查找  left=0  right=n
>
>关键点就是  **while(left+1<right)**      如果不这么写那么退出循环的时候就不正确了呢 







## [分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)

>```xml
>给定一个非负整数数组 `nums` 和一个整数 `m` ，你需要将这个数组分成 `m` 个非空的连续子数组。
>设计一个算法使得这 `m` 个子数组各自和的最大值最小。
>
>输入：nums = [7,2,5,10,8], m = 2
>输出：18
>一共有四种方法将 nums 分割为 2 个子数组。 其中最好的方式是将其分为 [7,2,5] 和 [10,8] 。
>因为此时这两个子数组各自的和的最大值为18，在所有情况中最小。
>```
>
>题目意思就是：分割子数组 并且分割出来的最大值是最小的呢  
>
>这个题目二分可不好找呢 在这里需要一点技巧。



## [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)



## [搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

>跟上边搜索旋转数组不一样的是  这里边带重复元素
>
>需要`nums[mid]==nums[left] left++`



## [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

>```java
>       if(nums[mid]>nums[right])
>           left=mid+1;
>       else
>           right=mid;
>```
>
>时间复杂度 logn



## [寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

>```java
>       if(nums[mid]>nums[right])
>           left=mid+1;
>       else if(nums[mid]<nums[right])
>           right=mid;
>       else if(nums[mid]==nums[right])
>           right--;
>```
>
>跟上述处理的方式就是在相等的时候处理结果要不同的呗 在这里哈呢





## [在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

>这里边存在重复数字  
>
>我们要二分查找左右两遍对应的数字起始位置 这个是算数字



## [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

>返回起始位置 和 终止位置
>
>这里边就是需要 左边查询和右边查询呗











# ==---------------------------------------------------------------DP==

# ==背包问题总结==

>#### 背包递推公式
>
>问能否装满背包 或者 最多装多少 `dp[j]=Math.max(dp[j],dp[j-nums[i]]+nums[i])`    对应题目
>
>- `ACM01背包`  
>- `416.`分割等和子集  
>- `1049.`最后一块石头的重量II
>
>----------------------
>
>-------------
>
>问装满背包有几种方案：`dp[j]=dp[j]+dp[j-nums[i]`   一定要初始化`dp[0]=1`
>
>- `494`.目标和
>- `518`.零钱兑换II
>- `377`.组合总和IV
>- `70`.爬楼梯进阶版
>
>----------------------
>
>---------------
>
>问背包装满最大价值：  `dp[j]=Math.max(dp[j],dp[j-weight[i]]+value[i])`
>
>- `474`.一和零  这个题比较难
>
>--------------
>
>--------------
>
>问装满背包所有物品的最小个数： `dp[j]=Math.min(dp[j],dp[j-coin]+1)`  一定要初始化`dp[0]=0`  并且`Arrays.fill(dp,target+1)`
>
>- `322`.零钱兑换
>- `279`.完全平方数
>
>--------------
>
>-------------
>
>#### 遍历顺序
>
>`01`背包：
>
>二维`d`p数组`01`背包先遍历物品还是先遍历背包都是可以的，且第二层`for`循环时重小到大遍历
>
>一维`dp`数组`01`背包只能先遍历物品在遍历背包容量，且第二层`for`循环是从大到小遍历
>
>-----------------
>
>-----------
>
>完全背包：
>
>纯完全背包问题，先遍历物品还是先遍历背包都是可以的，且第二层`for`循环时从小到大遍历  
>
>如果求组合数就是外层for循环遍历物品，内层for循环遍历背包。
>
>如果求排列数就是外层for循环遍历背包，内层for循环遍历物品。
>
>- 求组合数：518.零钱兑换II 
>- 求排列数： 377.组合总和IV   
>- 求最小数： 322.零钱兑换 279.完全平方数  两层for循环遍历顺序就无所谓了



# ==01背包==

> 物品数量为N 背包容积为V    v[]表示物品体积 w[]表示物品价值     01背包表示每个物品就是选择或者不选 在不超过容积的情况下 使价值最大呗
>
> 重点:
>
> - 递推公式： 二维 `dp[i][j]=Math.max(dp[i-1][j], dp[i-1][j-[v[i]] + w[i])`   表示从下标为【0-i】的物品里任意取，放进容量为j的背包
>
>  ​		                  一维 `dp[j]=Math.max(dp[j],dp[j-v[i]]+w[i])`     								 表示容量为j的背包所背的最大价值
>
> - 初始化：    对于只有正数的价值  非0下标初始化为0   对于有负数的价值 非0下标初始化为负无穷
> - 遍历顺序：二维初始化考虑倒叙遍历体积   以及一维遍历的时候  防止物品重复放入 倒叙进行遍历 
> - `for`循环嵌套顺序：二维情况下，不论先物品还是背包，都是依赖于左上角的值，所以不论怎么遍历都可以
> - **不论一维数组还是二维数组：在初始化容量的时候都需要+1  要学会dp初始化呗 **
>
> --------------------------
>
> 二维 一维遍历模板  **适合用于求最大值  以及 求正好为目标值** 只不过在这里就是dp含义就是定义得不一样呗 
>
> ```java
> for(int i=0; i<N; i++){
>     for(int j=0; j<=V; j++){
>         dp[i][j]=dp[i-1][j];
>         if(j>=vi[i]) dp[i][j]=Math.max(dp[i][j],dp[i-1][j-v[i]]+wi[i]);	 //01背包情况下  不选择  vs   选择
>     }
> }
> 
> 
> for(int i=0; i<N; i++){										//一维dp情况下 两个for循环不允许颠倒
>     for(int j=V; j>=weight[i]; j--){						//重大往小遍历 保证每种物品只被遍历一次
>         dp[j]=Math.max(dp[j], dp[j-weight[i]]+value[i]);  	//有时候weight[i]==value[i] 	
>     }
> }
> ```
>
> -----------------------
>
> 下边这种模板就是求组合方案数 类似于组数总和、目标和  `dp[j]=dp[j]+dp[j-nums[i]] 方案数 不选择  vs   选择`
>
> ```java
> //dp[i]表示容量为j的背包，有dp[j]种方案呗  在这里哈呢	dp[j]=dp[j-nums[i]]+dp[j];表示第i个元素不选择方案数+第i个元素选择方案数
> dp[0]=1;    //在这里dp[0]必须要初始化 否则后续递归所有值都为0  dp[0]就是代表容量为j 什么都不选我们所得方案数就是为1
> for(int i=0; i<nums.length-1; i++){
>     for(int j=weight; i>=nums[i]; j--){		//遍历顺序在这里就是一定要遵循01背包的模板定义哈
>         dp[j]=dp[j]+dp[j-nums[i]];
>     }
> }
> 
> ```

## [01背包ACM](https://www.acwing.com/problem/content/description/2/)

>```xml
>4 5   N=4 V=5
>1 2
>2 4
>3 4
>4 5
>```
>
>二维数组
>
>```java
>import java.util.Scanner;
>
>public class Main{
>    
>       public static void main(String[] args) throws Exception {
>           Scanner reader = new Scanner(System.in);
>           
>           int N=reader.nextInt();  //物品数量为4
>           
>           int V=reader.nextInt();  //背包容积为5
>           
>           int[] v=new int[N+1];    // 数组v 代表第i个元素的体积
>           int[] w=new int[N+1];    // 数组w 代表第i个元素的价值
>           
>         for (int i=1 ; i <= N ; i++){
>                                    // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
>                 v[i] = reader.nextInt();
>                 w[i] = reader.nextInt();
>           }
>           reader.close();
>        
>           
>          // 正式工作的代码
>           /*
>           定义一个二阶矩阵dp[N+1][V+1],
>           这里之所以要N+1和V+1，是因为第0行表示只能选择第0个物品的时候，即没有物品的时候
>        第0列表示背包的体积为0的时候，即不能装任何东西的时候
>   
>           dp[i][j]表示在 只能选择前i个物品，背包容量为j的情况下，背包中物品的最大价值
>         对于dp[i][j]有两种情况：
>         1. 不选择当前的第i件物品/第i件物品比背包容量要大，则dp[i][j] = dp[i-1][j]
>         2. 选择当前的第i件物品（潜在要求第i件物品体积小于等于背包总容量），则能装入的物品最大价值为：
>             当前物品的价值 加上 背包剩余容量在只能选前i-1件物品的情况下的最大价值
>             dp[i][j] = dp[i-1][j-v[i]] + w[i]
>         dp[i][j]在两种情况中选择比较大的情况作为当前的最优解；
>         即：
>         if(j >= v[i]):
>             dp[i][j] = max(dp[i-1][j], dp[i-1][j-v[i]] + w[i])
>         else:
>             dp[i][j] = dp[i-1][j]
>         */
> 
>         int[][] dp=new int[N+1][V+1];
>         dp[0][0]=0;
>         for(int i=1; i<=N; i++){
>             for(int j=0; j<=V; j++){
>                 
>                 if(v[i]<=j){          //这里边j就是代表当前体积容量为j的时候 我们可以装入的最大值呗 在这里哈呢
>                     dp[i][j]=Math.max(dp[i-1][j],dp[i-1][j-v[i]]+w[i]);
>                 }
>                 else{
>                     dp[i][j]=dp[i-1][j];  //这里就是不做选择 维持上一个选择呗 在这里哈呢
>                 }
>            }
>        }
>        System.out.println(dp[N][V]);
>         
>    }
>}
>```
>
>-----
>
>一维数组：
> 
> ```java
> import java.util.Scanner;
> 
> public class Main{
>   public static void main(String[] args) throws Exception {
>       // 读入数据的代码
>       Scanner reader = new Scanner(System.in);
>       // 物品的数量为N
>       int N = reader.nextInt();
>       // 背包的容量为V
>      int V = reader.nextInt();
>       // 一个长度为N的数组，第i个元素表示第i个物品的体积；
>       int[] v = new int[N + 1] ;
>       // 一个长度为N的数组，第i个元素表示第i个物品的价值；
>       int[] w = new int[N + 1] ;
> 
>       for (int i=1 ; i <= N ; i++){
>          // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
>           v[i] = reader.nextInt();
>           w[i] = reader.nextInt();
>       }
>       reader.close() ;
>
>       // 正式算法的代码
>       // 将dp优化为一维数组
>       /*
>      注意，这里第二层循环的时候，还是小到大循环的话，那么
> 
>       dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-v[i]] + w[i])
>      实际上变成了
>       dp[i][j] = Math.max(dp[i][j], dp[i][j-v[i]] + w[i]);
> 
>       因为i-1的值已经在前面被更新过了，覆盖了
>       为了避免这个问题，所以要逆序更新，即先更新第i个，然后更新第i-1个，从而保证第i-1个不被覆盖
> 
>       如果不逆序的话，输出结果为10，dp数组实际为：
>       0 0 0 0 0 0 
>       0 2 4 6 8 10
>       0 2 4 6 8 10
>       0 2 4 6 8 10
>       0 2 4 6 8 10
>       */
>       int[] dp = new int[V+1];
>       dp[0] = 0;
>       for(int i = 1; i <= N; i++){
>           for(int j = V; j >= v[i]; j--){
>               dp[j] = Math.max(dp[j], dp[j-v[i]] + w[i]);
>           }
>       }
>       System.out.println(dp[V]);
>   }
>}
>```





## [数字组合方案数](https://www.acwing.com/problem/content/280/)

>```xml
>给定 N 个正整数 A1,A2,…,AN，从中选出若干个数，使它们的和为 M，求有多少种选择方案。
>4 4
>1 1 2 2     返回结果就是3  	dp[i][j]就是在总和为j的情况下 在前i个元素当中进行选择可得的方案数倍
>```
>
>```java
>private static int groupNum(int[] nums, int sum) {
>   int len = nums.length;
>   int[] dp = new int[sum + 1];
>
>   dp[0] = 1;                                              //虽然在这里就是我们也要严格指定初始化条件呗 在这里哈呢 对吧哈
>   for (int i = 0; i < len; i++) {
>       for (int j = sum; j >= nums[i]; j--) {
>           dp[j] = dp[j] + dp[j - nums[i]];
>       }
>   }
>   return dp[sum];
>}
>```
>
>



## [目标和](https://leetcode-cn.com/problems/target-sum/)

>1. 首先在这里就是目标数s不知道是正是负呢 
>2. .其次这里边就是要寻找的是方案数 不是最大或者就是最小
>3. dp数组在这里就是需要该怎么初始化就是一个问题被
>
>------------------
>
>当遇到上述这种困难 就是转化一下题解思路倍 在这里哈呢   通过数学公式推导重而推导出01背包问题倍 在这里哈呢



>数字总和 和目标数  在这里求解的是方案数呗  当遇到第i个物品有选择一种方案 还有不进行选择的一种方案  在dp上要显示出来呗 在这里哈呢   重点

-------------



## [分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

>1. 正常思路 二维`boolean`数组进行判断 
>2. 完全按照01背包思路来求解   二维求解             有初始值       因为这里边就是正序进行遍历 所以必须要初始值被  
>3. 按照01背包                             一维求解          没有初始值   因为在这里边是倒叙进行遍历 所以就是不需要初始化



## [最后一块石头的重量 II](https://leetcode-cn.com/problems/last-stone-weight-ii/)

>跟分割等和子集就是非常类似 还是完全就是采用01背包模板 



## [一和零](https://leetcode-cn.com/problems/ones-and-zeroes/)

>在这里就是非常难点呗 就是看如何转化为01背包呢 在这里哈呢
>
>m n 就是背包得长度和宽度限制呗在这里哈呢



# ==完全背包==

## [完全背包ACM](https://www.acwing.com/problem/content/description/3/)

>每件物品都有无限个，也就是可以放入背包多次，求解将哪些物品放入背包里得物品价值总和最大
>
>完全背包和01背包问题唯一不同得地方就是，每种物品有无线个
>
>01背包内嵌得循环是重大到小遍历，为了保证每个物品仅被添加一次。完全背包得物品时可以添加多次得，所以要重小到大去遍历。
>
>二维模板
>
>```java
>int[][] dp=new int[N+1][V+1];
>for(int i=1; i<=N; i++){
>for(int j=0; j<=V;j++){
>   dp[i][j]=dp[i-1][j];
>   if(j>=vi[i]) dp[i][j]=Math.max(dp[i][j],dp[i][j-vi[i]]+w[i]); //不同点只有在dp[i][j-vi[i]]+wi[i] 还是在前i个物品当中选择
>}
>}
>```
>
>![image-20210517101727164](C:\Users\whig\AppData\Roaming\Typora\typora-user-images\image-20210517101727164.png)
>
>一维模板
>
>```java
>int[] dp=new int[V+1]; //表示容量为j的情况下 可以凑成的最大价值
>for(int i=0; i<N; i++){
>for(int j=vi[i]; j<=V; j++){
>   dp[j]=Math.max(dp[j],dp[j-vi[i]]+wi[i]);       //注意for(j==vi[i])重这里开始遍历的呢	 也可以重0开始 if(j>=vi[i])加条件	
>}
>}
>//01背包下 for(int j=V; j>=vi[i]; j--) 遍历顺序是颠倒过来的 所以需要注意在这里哈呢
>```
>
>------------------
>
>遍历顺序：
>
>组合不强调元素之间得顺序，排列强调元素之间得顺序    `dp[j]=dp[j]+dp[j-nums[i]] 跟01背包模板一样就是求组合数 不是求排列数`
>
>- 先遍历物品 在遍历背包容量 得到的是组合数			  零钱兑换II
>- 先遍历背包容量 在遍历物品 得到的是排列数              组合总和IV
>
>---------------------------------
>
>-----------------------
>
>初始化：
>
>求解方案数的时候  `dp[j]=dp[j]+dp[j-nums[i]`  在这里边`dp[0]=1` 一定要初始化为1呢 在这里
>
>最大值 正常全部初始化为0 就可以了呢在这里哈呢
>
>最小值  `Arrays.fill(dp,max)---》dp[0]=0`







## [完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

>这个其实跟零钱兑换的思路是一摸一样的
>
>难点： `dp[0]==0` 初始化一定要正确   并且需要进行一下优化代码呢 在这里哈呢

## [零钱兑换最小硬币个数](https://leetcode-cn.com/problems/coin-change/)

>1. 难点 题目要求是最小硬币个数 不是求最多
>2. 初始化选择 就遇到难点了   不能初始化成`Integer.MAX_VALUE`否则就是在相加的时候编程负无穷
>3. for循环嵌套也是难点了       组合数排列数 在这里就是都可以 
>
>-------------
>
>初始化时难点

## [零钱兑换 II 组合数方案](https://leetcode-cn.com/problems/coin-change-2/)

>本题就是求组合数，要想着递推公式`dp[j]=dp[j]+dp[j-nums[i]] 并且要弄懂遍历顺序`  这种就不是完全背包了 求能否装满背包 求装满背包有几种方式
>
>- 如果求组合数 就是外层for循环遍历物品   内层for循环遍历背包
>- 如果求排列数 就是外层for循环遍历背包   内层for循环遍历物品     
>
>---------------------------
>
>这个零钱兑换II 当作一个模板 就是在这里就是太重要了啊  非常重要 求组合数 
>
>```java
>for (int i = 0; i < coins.size(); i++) { // 遍历物品
>   for (int j = coins[i]; j <= amount; j++) { // 遍历背包容量
>       dp[j] += dp[j - coins[i]];
>   }
>}
>```
>
>假设：coins[0] = 1，coins[1] = 5。
>
>那么就是先把1加入计算，然后再把5加入计算，得到的方法数量只有{1, 5}这种情况。而不会出现{5, 1}的情况。
>
>**所以这种遍历顺序中dp[j]里计算的是组合数！**
>
>如果把两个for交换顺序，代码如下：
>
>```
>for (int j = 0; j <= amount; j++) { // 遍历背包容量
>   for (int i = 0; i < coins.size(); i++) { // 遍历物品
>       if (j - coins[i] >= 0) dp[j] += dp[j - coins[i]];
>   }
>}
>```
>
>背包容量的每一个值，都是经过 1 和 5 的计算，包含了{1, 5} 和 {5, 1}两种情况。
>
>**此时dp[j]里算出来的就是排列数！**



## [组合总和 Ⅳ](https://leetcode-cn.com/problems/combination-sum-iv/)

>```xml
>输入：nums = [1,2,3], target = 4
>输出：7
>解释：
>所有可能的组合为：
>(1, 1, 1, 1)
>(1, 1, 2)
>(1, 2, 1)
>(1, 3)
>(2, 1, 1)
>(2, 2)
>(3, 1)
>```
>
>这个就是求解排列数  跟组合不一样  但是`dp定义都一样  dp[j]=dp[j]+dp[j-nums[i]]`
>
>**完全背包：先遍历背包 在遍历物品   求解排列方案数**



## [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

>1. 斐波那契数列一种解法  `dp[i]=dp[i-1]+dp[i-2]`
>2. 完全背包一种解法  求解排列组合呢 --->`dp[0]==1`



## [把数字翻译成字符串的方案数](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

>跟爬楼梯 在这里就是类似的呢





## [斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

## [三步问题](https://leetcode-cn.com/problems/three-steps-problem-lcci/)







## [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

>一点资讯笔试题



# ==股票系列==

## [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

>只能一次进行买入和卖出
>
>```xml
>输入：[7,1,5,3,6,4]
>输出：5
>解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
>注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
>```
>
>思路： 定义两个变量就是可以  一个就是买入 一个就是卖出
>
>```java
>for(int i=0; i<len; i++){
>buy=Math.min(buy, nums[i]);
>res=Math.max(res, nums[i]-buy);
>}
>```



## [买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

>手里可持有一只股票 但是可以多次进行买入和卖出
>
>```java
>输入: prices = [7,1,5,3,6,4]
>输出: 7
>解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
>     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
>```
>
>```java
>// 贪心算法思想呗 这个点只要存在上坡 前一个节点买入  后一个节点就是卖出
>public int maxProfit(int[] prices) {
>   int res = 0;
>   for(int i = 1;i < prices.length;++i){
>       if(prices[i] > prices[i-1]) res += prices[i] - prices[i-1];
>   }
>   return res;
>}
>```
>
>
>
>

## [买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

>最多可以交易两笔



## [买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

>最多可以完成K笔交易呗  在这里哈呢





## [最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

## [买卖股票的最佳时机含手续费](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

## [鸡蛋掉落 高频笔试](https://leetcode-cn.com/problems/super-egg-drop/)



# ==打家劫舍==



## [打家劫舍](https://leetcode-cn.com/problems/house-robber/)

## 打家劫舍-字节面试-可以携款潜逃

>在上边的基础上 就是可以进行携款潜逃触发报警 问可以取得的最大值
>
>public static void main(String[] args) {
>   int[] nums = {7, 5, 4, 2, 3};
>   System.out.println(findMoney(nums));
>   System.out.println(findMoney1(nums));
>}
>
>```java
>private static int findMoney(int[] nums) {
>if (nums == null) return 0;
>int len = nums.length;
>if (len == 0) return 0;
>if (len == 1) return nums[0];
>if (len == 2) return nums[0] + nums[1];
>
>int[] dp = new int[len];           //代表以 i 为结尾 获取到的最大值
>dp[0] = nums[0];
>dp[1] = Math.max(nums[0], nums[1]);
>
>int res = 0;  //这里边就是可以连续偷  但是在这里就是会触发报警 就不能再偷了呢
>for (int i = 2; i < len; i++) {
>   dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
>   res = Math.max(res, Math.max(dp[i - 1] + nums[i], dp[i - 2] + nums[i]));   //这里边就是找连续偷 和 不连续偷的最大值呗
>}
>return res;
>}
>
>// 小偷 偷钱 再次进行空间上上进行优化
>private static int findMoney1(int[] nums) {
>if (nums == null) return 0;
>int len = nums.length;
>if (len == 0) return 0;
>if (len == 1) return nums[0];
>if (len == 2) return nums[0] + nums[1];
>
>int[] dp = new int[len];           //代表以 i 为结尾 获取到的最大值
>dp[0] = nums[0];
>dp[1] = Math.max(nums[0], nums[1]);
>int first = nums[0];
>int second = Math.max(nums[0], nums[1]);
>int cur = 0;
>
>int res = 0;  //这里边就是可以连续偷  但是在这里就是会触发报警 就不能再偷了呢
>for (int i = 2; i < len; i++) {
>   cur = Math.max(second, first + nums[i]);
>   res = Math.max(res, Math.max(second + nums[i], first + nums[i]));
>   first = second;
>   second = cur;
>}
>return res;
>}
>```



## [打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

## [打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)



# ==路径问题==

## [机器人 不同路径](https://leetcode-cn.com/problems/unique-paths/)

## [机器人 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

>这里边就是有障碍 跟上边就是稍微不一致呢 
>
>分析四种情况呗



## [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

## [礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

>礼物最大价值 跟 最小路径和 在这里就是一样的呢

## [三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

>```xml
>输入：triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
>输出：11
>解释：如下面简图所示：
>2
>3 4
>6 5 7
>4 1 8 3
>自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。
>```
>
>底部向上 进行dp遍历



# ==数组子序列问题==



## 数组中左边最大、右边最小的元素

>```
>//输入：[2, 3, 1, 8, 9, 20, 12]
>//输出：3, 4
>//解释：数组中 8, 9 满足题目要求，他们的索引分别是 3、4
>```
>
>思路： 1. 要求时间复杂度 O(N)  我们在这里就是该怎么办呗 
>
>   		 2. 就是再新建立两个数组 一个表示当前元素左边最大值  一个表示当前元素右边最大值呗
>   	 	 3. 这种做法就是典型的时间换取空间被  
>
>```java
> public static List<Integer> find(int[] nums) {
>        //找到左边数字比较当前数字小 右边数字比当前数字大的两个数组呗
>        //这种就是进行时间上的优化 我们就是可以使用空间进行优化呗 在这里哈呢
>        int len = nums.length;
>        int[] left_max = new int[len];          //[0,i)     最大的      并且在这里边数组需要初始值 最小值呢
>        int[] right_min = new int[len];         //(i,len-1] 中最下的    在这里数组需要初始值最大值呢 在这里哈呢
>        Arrays.fill(left_max, Integer.MIN_VALUE);
>        Arrays.fill(right_min, Integer.MAX_VALUE);
>        for (int i = 1; i < len; i++) {
>            left_max[i] = Math.max(left_max[i - 1], nums[i - 1]);
>        }
>        for (int i = len - 2; i >= 0; i--) {
>            right_min[i] = Math.min(nums[i + 1], right_min[i + 1]);  //后续遍历 在这里我们找到右边最小值呗
>        }
>        List<Integer> list = new ArrayList<>();
>        for (int i = 0; i < len; i++) {
>            if (left_max[i] < nums[i] && nums[i] < right_min[i]) {
>                list.add(i);
>            }
>        }
>        return list;
>    }
>```



## [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

>```
>输入: [2,3,-2,4]
>输出: 6
>解释: 子数组 [2,3] 有最大乘积 6。
>```
>
>思路： 差不多也是采用动态规划 但是在这里两个变量就是可以维持一下呗
>
>1. 遍历数组时，记录当前最大值 并不断更新
>2. 我们就是需要维持两个变量  一个是最大值 一个是最下值
>3. 当遇到负数的时候 最大值和最小值进行交换  
>4. 并且维持一个变量  在遍历的时候就是更新当前连续子数组最大值呗



## [最长重复子数组](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/)

>```
>输入：
>A: [1,2,3,2,1]
>B: [3,2,1,4,7]
>输出：3
>长度最长的公共子数组是 [3, 2, 1] 。
>```
>
>思路：
>
>```xml
>    1.dp[i][j] 表示以i为结尾的A数组 和以j为结尾的B数组 的最长重复数组
>    2.dp[i][j]--->  if(nums[i]==nums[j]) dp[i][j]=dp[i-1][j-1]+1;    else{dp[i][j]==0}
>    3.由于这里边用到 dp[i-1][j-1] 所以我们需要就是初始化长度需要大一些
>```
>
>----
>
>时间复杂度:   O(n^2)
>
>空间复杂度：O(1)





## [最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

>```
>输入：text1 = "abcde", text2 = "ace" 
>输出：3  
>解释：最长公共子序列是 "ace" ，它的长度为 3 。
>```
>
>思路：
>
>```xml
>    1.这里边最长公共子序列 就是最长公共子数组是不一样的 最长子数组是连续的 在这里不是连续的呢
>    2.dp[i][j] 表示以i 为结尾txt1 和以 J为结果txt2 的最长公共子序列呗    因为这里边就是需要dp[i-1][j-1] 所以初始化长度大一
>		3.if(nums[i-1]==nums[j-1]) dp[i][j]=dp[i-1][j-1]+1
>		  else 										 dp[i][j]=Math.max(dp[i-1][j],dp[i][j-1]);
>```
>
>----
>
>时间复杂度： O(N^2)
>
>空间复杂度:   O(1)



## [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

>```
>输入：nums = [10,9,2,5,3,7,101,18]
>解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。
>```
>
>思路：
>
>```xml
>dp[i] 表示以 nums[i] 结尾的最长上升子序列的长度。即：在 [0, .., i] 的范围内，选择以数字 nums[i] 结尾可以获得的最长上升子序列的长度。
>
>遍历到 nums[i] 的时候，我们应该把下标区间 [0, ... ,i - 1] 的 dp 值都看一遍，如果当前的数 nums[i] 大于之前的某个数，那么 nums[i] 就可以接在这个数后面形成一个更长的上升子序列。把前边dp[i]中最大的拿出来进行+1 操作 
>
>并且dp初始值 一定要全赋值为1呢 在这里哈呢 
>    for (int i = 1; i < len; i++) {
>            for (int j = 0; j < i; j++) {
>                if (nums[j] < nums[i]) {
>                    dp[i] = Math.max(dp[j] + 1, dp[i]);
>                }
>            }
>     }                                 
>```
>
>-----
>
>时间复杂度：O(N^2)
>
>空间复杂度：O(n^2)



## [最长连续递增序列](https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/)

>```xml
>输入：nums = [1,3,5,4,7]
>输出：3
>解释：最长连续递增序列是 [1,3,5], 长度为3。
>```
>
>思路：
>
>```xml
>这种跟最长递增序列是不一样呢。。 因为这里边可以进行连续操作呢  所以不用找[0...i]中最大的递增子序列 只需要往下排动就是可以了呢
>Arrays.fill(dp,1);
>1. if(nums[i]>nums[i-1]) dp[i]=dp[i-1]+1   更新res最大值
>```
>
>-----
>
>时间复杂度：O(N)
>
>空间复杂度：O(N)
>
>-------
>
>思路2：
>
>```xml
>可以不用试动态规划 只需要用一个count来维持记录就是可以呢
>            if(nums[i]>nums[i-1]){
>                count++;
>                res=Math.max(res,count);
>            }
>            else{
>                count=1;
>            }
>```

## [最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)



# ==笔试&&难题==

## [最多可以参加的会议数目](https://leetcode-cn.com/problems/maximum-number-of-events-that-can-be-attended/)

## [最多可以参加的会议数目 II](https://leetcode-cn.com/problems/maximum-number-of-events-that-can-be-attended-ii/)

> `dp` 有价值的 并且在这里进行加权重了呢

## [规划兼职工作](https://leetcode-cn.com/problems/maximum-profit-in-job-scheduling/)

## [正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

## [最大正方形](https://leetcode-cn.com/problems/maximal-square/)

## [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

## [回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

## A B C 串交错形成  原创

>```xml
>给定三个字符串 s1、s2、s3，请你帮忙验证 s3 是否是由 s1 和 s2 交错 组成的。
>输入：s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac" 
>输出：true
>```
>
>```java
>public static boolean isABC(String s1, String s2, String s3) {
>
>//这里边双指针就是会造成一种困扰呢 在这里哈呢
>int len1 = s1.length(), len2 = s2.length(), len3 = s3.length();
>if (len3 != (len1 + len2)) return false;
>
>boolean[][] dp = new boolean[len1 + 1][len2 + 1];  //dp[i][j]  s1 前 i 个字符与 s2 前 j 个字符能否交错形成 s3 前 i + j 个字符。
>
>//dp[i]][j] = (dp[i-1][j] && s1[i-1] == s3[i+j-1]) || (dp[i][j-1] && s2[j-1] == s3[i+j-1])
>dp[0][0] = true;   //因为 "" 和 "" 可以形成""
>for (int i = 0; i <= len1; i++) {
>  for (int j = 0; j <= len2; j++) {
>      if (i >= 1) dp[i][j] = dp[i][j] || dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1);
>      if (j >= 1) dp[i][j] = dp[i][j] || dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1);
>  }
>}
>System.out.println(Arrays.deepToString(dp));
>return dp[len1][len2];
>}
>```



## [正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

>1. 这个就是动态规划系列呗 太难了  先放一放呗

# ==---------------------------------------------------------------贪心==

>贪心的本质是选择每一阶段的局部最优，从而达到全局最优,你有一个背包体积为n，如何把背包尽可能装满，如果每次还选择最大，就不行了。这时候就需要动态规划。
>
>刷题或者面试的时候，手动模拟一下感觉可以局部最优推出整体最优，而且想不到反例，那么就试一试贪心。
>
>所以这也是为什么很多同学通过（accept）了贪心的题目，但都不知道自己用了贪心算法，因为贪心有时候就是常识性的推导，所以会认为本应该就这么做！
>
>- 将问题分解为若干个子问题
>- 找出适合的贪心策略
>- 求解每一个子问题的最优解
>- 将局部最优解堆叠成全局最优解



## [分发饼干](https://leetcode-cn.com/problems/assign-cookies/)

>1. 首先数组在这里边我们就是需要进行一下排序呗 
>2. 其次我们使用贪心算法 一定要决定自己贪心的策略 怎么是局部最优 怎么才能是全局最优呢
>3. 其次 在这里遍历谁的顺序也比较重要  如果能用`for`循环就使用`for`循环 不能使用`for`循环 我们在这里就是使用`while`循环呗
>4. 同时看到两个数组 不一定非得使用两个`for循环`如果是这样字的话，那么就是逻辑将会非常复杂呢 



## [摆动序列](https://leetcode-cn.com/problems/wiggle-subsequence/)

>1. 难点 思路知道但是代码写不出来  逐一去攻破呗 在这里哈呢
>2. 一个是递增序列 一个是递减序列 所以我们就是要用两个临时变量来保存一下呗 在这里哈呢



## [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

>1. 读题的感觉就是在这里有点难度呢 
>2. 贪心策略 每次选择跳跃最大长度就是可以了呢 
>3. 遍历上 `for(int i=0; i<=distance; i++)`  不一定就是要遍历完数组所有长度呗  因为有的路径是走不过去的呢





## [跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)





## [K 次取反后最大化的数组和](https://leetcode-cn.com/problems/maximize-sum-of-array-after-k-negations/)

>也是贪心思路 局部最优推导出全局最优呢 在这里哈呢
>
>同时遍历的时候采用变量来记录一下呗  并且怎么地呢 





## [加油站](https://leetcode-cn.com/problems/gas-station/)

>1. 因为这个题就是带有循环  所以在这里我们就是先暴力解法在这一下呢哈  暴力解法 这里边就是带有循环数组就是很有难度
>2. 贪心策略 一个是全局`sum`  一个是当前`sum`判断是否满足的就是当前条件呗 在这里哈呢



## [无重叠区间](https://leetcode-cn.com/problems/non-overlapping-intervals/)

>- 难点一：一看题就有感觉需要排序，但究竟怎么排序，按左边界排还是右边界排。
>- 难点二：排完序之后如何遍历，如果没有分析好遍历顺序，那么排序就没有意义了。
>- 难点三：直接求重复的区间是复杂的，转而求最大非重复区间个数。
>- 难点四：求最大非重复区间个数时，需要一个分割点来做标记。
>
>----------
>
>先做好排序规则 之后就是在进行比较呗 





## [最多可以参加的会议数目](https://leetcode-cn.com/problems/maximum-number-of-events-that-can-be-attended/)

>```xml
>输入：events = [[1,2],[2,3],[3,4]]       [i,j]表示会议第i天开始  第j天结束
>输出：3
>
>特殊例子：  [[1,2][1,5], [2,4], [3,4]]
>```
>
>思路：
>
>1. 首先要使用贪心思想：我们要参加最早结束的会议
>2. 其次是对事件进行排序：排序规则 是先以结束`j nums[1]`进行排序  如果`nums[j]`一样 我们再以`nums[i]`进行排序
>3. `Arrays.sort(nums, (o1,o2)-> o1[1]==o2[1]? o1[0]-o2[0]:o1[1]-o2[1])` 
>4. 其次我们利用`HashSet 或者 boolean[]数组`来按断是否添加重复的日程
>



# ==---------------------------------------------------------------string==





# ==字符串相加、相减、相乘、16进制==



## [把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

>这里边假如就是面试题： 我们就是要考虑以下几点异常呗
>
>1. 字符串是否为空呢 在这里哈呢
>2. 是否有空格
>3. 字符串是否是非法的
>4. 超出`int`类型怎么办
>5. 是不是有正负号之分 
>
>----------
>
>思路：
>
>1. 首先是去除空格
>2. 判断正负号  防止"+-2" 这种测试案例 必须要使用 `if else if`
>3. 判断是否是数字`Character.isDigit(char c)`
>4. 用 long 类型数字来接受  并判断是否是大于`Integer.MAX_VALUE`  并把正负号在这里带上呢 

## 大数字符串相加

>1. 首先表示进制位  carry来表示
>2. 其次这个字符串全都是数字没有正负号
>3. 再者返回类型在这里就是`int`类型呢
>
>```java
>    //首先要一下这里边就是有非法数字么  还有不带负号和+号么 返回值类型用String来表示呗
>    public static String add(String str1, String str2) {
>        int len1 = str1.length(), len2 = str2.length();
>        int carry = 0, l1 = len1 - 1, l2 = len2 - 1;
>
>        StringBuilder sb = new StringBuilder();
>        while (l1 >= 0 && l2 >= 0) {
>            int num1 = str1.charAt(l1--) - '0';
>            int num2 = str2.charAt(l2--) - '0';
>            int sum = num1 + num2 + carry;
>            sb.append(sum % 10);
>            carry = sum / 10;
>        }
>
>        while (l1 >= 0 || l2 >= 0 || carry > 0) {
>            if (l1 >= 0) {
>                int num1 = str1.charAt(l1--) - '0';
>                int sum = num1 + carry;
>                sb.append(sum % 10);
>                carry = sum / 10;
>            } else if (l2 >= 0) {
>                int num1 = str1.charAt(l2--) - '0';
>                int sum = num1 + carry;
>                sb.append(sum % 10);
>                carry = sum / 10;
>            } else {
>                sb.append(1);
>                break;
>            }
>        }
>        return sb.reverse().toString();
>    }
>```



## 大数字符串相减

>1. 首先判断字符串长度是否一直    我们设计一个函数就是专门进行大数减小数呗
>2. 这时候分三种情况  大于 等于 小于 
>3. 字符串长度相等的时候又分三种情况  利用`String 函数中 compare `方法做判断就好了呢
>
>```java
>   public static String subStrings(String str1, String str2) {
>        int len1 = str1.length(), len2 = str2.length();
>        if (len1 < len2) return "-" + sub(str2, str1);
>        if (len1 > len2) return sub(str1, str2);
>        if (len1 == len2) {
>            int cmp = str1.compareTo(str2);
>            if (cmp == 0) return "0";
>            if (cmp > 0) return sub(str1, str2);
>            if (cmp < 0) return "-" + sub(str2, str1);
>        }
>        return "";
>    }
>
>    //这里边实现相当于大数减小数呗
>    public static String sub(String a, String b) {
>        StringBuilder sb = new StringBuilder();
>        int borrow = 0;
>        int i = a.length() - 1, j = b.length() - 1;
>        while (i >= 0 || j >= 0) {
>            int x = i >= 0 ? a.charAt(i--) - '0' : 0;
>            int y = j >= 0 ? b.charAt(j--) - '0' : 0;
>            int z = (x - borrow - y + 10) % 10;
>            sb.append(z);
>            borrow = x - borrow - y < 0 ? 1 : 0;
>        }
>        sb.reverse();
>        //删除前导0。循环条件是res.size()-1是为防止"0000"的情况
>        //例如，当121-120=001，需要将前面的0删除，得到最终结果1。
>        //注意121-121=000这种情况，不要把所有0都删了！
>        int pos;
>        for (pos = 0; pos < sb.length() - 1; pos++) {   //位置就是长度-1 这里边判断是没是有前倒0倍
>            if (sb.charAt(pos) != '0') break;
>        }
>        return sb.substring(pos);
>    }
>```



## [字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

>1. 数组存放上次的计算结果。因为被乘数每一位数字和乘数相乘的结果是依次错开的
>2. 其次 每一位在这里都是相乘呢
>
>```java
>        /**
>        num1的第i位(高位从0开始)和num2的第j位相乘的结果在乘积中的位置是[i+j, i+j+1]
>        例: 123 * 45,  123的第1位 2 和45的第0位 4 乘积 08 存放在结果的第[1, 2]位中
>          index:    0 1 2 3 4  
>              
>                        1 2 3
>                    *     4 5
>                    ---------
>                          1 5
>                        1 0
>                      0 5
>                    ---------
>                      0 6 1 5
>                        1 2
>                      0 8
>                    0 4
>                    ---------
>                    0 5 5 3 5
>        这样我们就可以单独都对每一位进行相乘计算把结果存入相应的index中        
>        **/    
>     public String multiply(String num1, String num2) {
>	
>        int n1 = num1.length()-1;
>        int n2 = num2.length()-1;
>        if(n1 < 0 || n2 < 0) return "";
>        int[] mul = new int[n1+n2+2];
>
>        for(int i = n1; i >= 0; --i) {
>            for(int j = n2; j >= 0; --j) {
>                int bitmul = (num1.charAt(i)-'0') * (num2.charAt(j)-'0');
>                bitmul += mul[i+j+1]; // 先加低位判断是否有新的进位
>                mul[i+j] += bitmul / 10;
>                mul[i+j+1] = bitmul % 10;
>            }
>        }
>
>        StringBuilder sb = new StringBuilder();
>        int i = 0;
>        // 去掉前导0
>        while(i < mul.length-1 && mul[i] == 0)
>            i++;
>        for(; i < mul.length; ++i)
>            sb.append(mul[i]);
>        return sb.toString();
>    }
>```



## [基本计算器 II](https://leetcode-cn.com/problems/basic-calculator-ii/)

>```
>输入：s = "3+2*2"
>输出：7
>```
>
>利用一个栈来记录数字  并用一个符号来记录前一个是什么符号





## 36进制加法

>```xml
>36进制由0-9，a-z，共36个字符表示，最小为’0’, ‘0’、'9’对应十进制的09，‘a’、'z’对应十进制的10 35
>
>'1b' 换算成10进制等于 1 * 36^1 + 11 * 36^0 = 36 + 11 = 47
>
>要求按照加法规则计算出任意两个36进制正整数的和
>
>如：按照加法规则，计算'1b' + '2x' = '48'
>
>要求：
>
>不允许把36进制数字整体转为10进制数字，计算出10进制数字的相加结果再转回为36进制
>```
>
>```java
>public class Test {
>    public static String add36BinString(String s1, String s2) {
>        int len1 = s1.length() - 1;
>        int len2 = s2.length() - 1;
>        int carry = 0;              //表示进位 满足36就是+1呗 在这里哈
>           StringBuilder sb = new StringBuilder();
>           while (len1 >= 0 || len2 >= 0 || carry > 0) {
>            int num1 = len1 >= 0 ? getInt(s1.charAt(len1--)) : 0;
>               int num2 = len2 >= 0 ? getInt(s2.charAt(len2--)) : 0;
>               int sum = num1 + num2 + carry;
>            carry = sum / 36;
>               sb.append(getChar(sum % 36));
>             }
>             return sb.reverse().toString();
>    }
>     
>    private static int getInt(char c) {
>             return '0' <= c && c <= '9' ? c - '0' : c - 'a' + 10;
>         }
>   
>    private static char getChar(int num) {
>           return (char) ((num <= 9) ? num + '0' : 'a' + num - 10);
>    }
>
>    public static void main(String[] args) {
>           System.out.println(add36BinString("1b", "2x"));   // ==48
>       }
>}
>```

## 36进制减法

>主要就是借位  ＋ 判断
>
>```java
>public class Test {
>    private static String sub36BinString(String s1, String s2) {
>        int len1 = s1.length() - 1;
>           int len2 = s2.length() - 1;
>           StringBuilder sb = new StringBuilder();
>           if (len1 > len2 || len1 == len2 && (s1.charAt(0) - '0') >= s2.charAt(0) - '0') {
>            return sub36Bin(s1, s2, len1, len2, sb);   //这里边相等的时候还是需要重新进行判断呗
>           }
>             sb.append('-');                                //作为标记 最后在判断
>           return sub36Bin(s2, s1, len2, len1, sb);
>       }
>   
>    /**
>     * @param s1 我们让s1>s2
>     */
>     private static String sub36Bin(String s1, String s2, int len1, int len2, StringBuilder sb) {
>         boolean borrow = false;  //true表示借位
>         while (len1 >= 0 && len2 >= 0) {
>             int num1 = len1 >= 0 ? getInt(s1.charAt(len1--)) : 0;
>            int num2 = len2 >= 0 ? getInt(s2.charAt(len2--)) : 0;
>             if (borrow) {
>                 num1 = num1 - 1;
>             }
>             if (num1 >= num2)
>                 sb.append(getChar((num1 - num2) % 36));  //这里边对 %36是多余的
>             else {
>                 borrow = true;   //产生借位
>                 num1 = num1 + 36;
>                 sb.append(getChar(num1 - num2));
>             }
>         }
> 
>         if (sb.charAt(sb.length() - 1) == '0') {
>             //>1解释  因为s1>=s2   如果sb中有'-'那么后续指定不能为0
>             while (sb.length() > 1 && sb.charAt(sb.length() - 1) == '0') {
>                sb.deleteCharAt(sb.length() - 1);        //删除多余的0  例如2000 - 2000
>             }
>         }
>         if (sb.charAt(0) == '-') {
>             sb.deleteCharAt(0);    //这里边主要因为返回结果我们就是要进行反转呗
>             sb.append('-');
>         }
>         return sb.reverse().toString();
>     }
> 
>     private static int getInt(char c) {
>         //通过数字返回进制呗 在这里哈
>         return '0' <= c && c <= '9' ? c - '0' : c - 'a' + 10;
>    }
> 
>     private static char getChar(int num) {
>         return (char) ((num <= 9) ? num + '0' : 'a' + num - 10);
>     }
>}
> ```



## [把数字翻译成字符串的方案数](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

> Dp 动态规划  类似于青蛙跳台阶问题



## [整数转罗马数字](https://leetcode-cn.com/problems/integer-to-roman/)

> 首先数字是有范围的 如果没有范围 在这里就是做不了呢
>
> 两个数字  `int[]-->String[] 映射`
>
> 遍历 `while`循环判断



## [罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/)

>使用`hashmap` 来配对判断呗 

# ==回文子串、子串==

## [验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

>思路：就是简单的双指针 但是要学`Character`中一些方法
>
>​			`Character.isLetterOrDigit` 	判断是否是字母或者是数字
>
>​			`Character.toUpperCase`		     只有字母的时候是大写转换 其他`char`类型就是不变
>
>​			`Character.toLowerCase`			 只有字母的时候是小写转换 其他`char`类型就是不变

## [验证回文字符串 可以进行删除一次](https://leetcode-cn.com/problems/valid-palindrome-ii/)

## [回文排列](https://leetcode-cn.com/problems/palindrome-permutation-lcci/)

## [最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)

>1. `int[] nums=new int[128]` 这个就是计数排序的形式呗  我们就是不采用`HashMap`了呗
>2. `HashMap`的时间复杂度比较高，所以我们在字符串处理的时候能用`int[]数组来表示就用int[]数组来表示呗`

## [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

>```
>输入：s = "babad"
>输出："bab"
>解释："aba" 同样是符合题意的答案。
>```
>
>思路：
>
>1. 利用中心扩散方法  遍历到一个点的时候就是调用辅助函数进行两遍 中心进行扩散
>2. 动态规划

## [判断有多少个回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

>```
>输入："aaa"
>输出：6
>解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"
>```
>
>1. 中心扩散方法
>2. 动态规划

## [最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

>```
>输入：s = "bbbab"
>输出：4
>解释：一个可能的最长回文子序列为 "bbbb" 。
>//子序列定义为：不改变剩余字符顺序的情况下，删除某些字符或者不删除任何字符形成的一个序列。
>/**
>d[i][i]=1
>当s[i]=s[j]                                  dp[i][j] = dp[i+1][j-1]+2 
>当s[i]!=s[j] 取s[i+1..j] 和s[i..j-1]中最长的   dp[i][j]=max(dp[i+1][j],dp[i][j-1]) 
>由于dp[i][j]需要dp[i+1][j]所以需要逆序枚举s的长度，而又因为j是递增的，所以在求解dp[i][j]时,dp[i][j-1]肯定已经求解过了
>*/
>```

----

## [重复的子字符串](https://leetcode-cn.com/problems/repeated-substring-pattern/)

>1. 枚举算法
>2. kmp算法 --->kmp优化算法呗 

## [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

>1. 滑动窗口秒杀   还可以使用更简单的办法就是`new int[128]`  下次再看看
>2. 这里边就是可以使用动态规划呗 

## [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

>1. 动态规划算法
>2. 中心扩展算法

## [至少有 K 个重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/)

>```
>输入：s = "ababbc", k = 2
>输出：5
>解释：最长子串为 "ababb" ，其中 'a' 重复了 2 次， 'b' 重复了 3 次。
>```
>
>思路：
>
>1. 进行 分治思想递归来求解  当某一个字符<k 的时候 对这个字符进行分割 之后递归求解最大值
>2. 滑动窗口思路 在这里就是不好想呢

# ==kmp==

## KMP算法流程

>- "前缀"和"后缀"。 "前缀"指除了最后一个字符以外，一个字符串的全部头部组合；"后缀"指除了第一个字符以外，一个字符串的全部尾部组合。
>
>- －　"A"的前缀和后缀都为空集，共有元素的长度为0；
>
> 　　－　"AB"的前缀为[A]，后缀为[B]，共有元素的长度为0；
>
> 　　－　"ABC"的前缀为[A, AB]，后缀为[BC, C]，共有元素的长度0；
>
> 　　－　"ABCD"的前缀为[A, AB, ABC]，后缀为[BCD, CD, D]，共有元素的长度为0；
>
> 　　－　"ABCDA"的前缀为[A, AB, ABC, ABCD]，后缀为[BCDA, CDA, DA, A]，共有元素为"A"，长度为1；
>
> 　　－　"ABCDAB"的前缀为[A, AB, ABC, ABCD, ABCDA]，后缀为[BCDAB, CDAB, DAB, AB, B]，共有元素为"AB"，长度为2；
>
> 　　－　"ABCDABD"的前缀为[A, AB, ABC, ABCD, ABCDA, ABCDAB]，后缀为[BCDABD, CDABD, DABD, ABD, BD, D]，共有元素的长度为0
>
>
>
> 算法流程：
>
>  1. 假设现在文本串`S`匹配到 `i `位置，模式串`P`匹配到` j` 位置
>  2. 如果`j = -1`，或者当前字符匹配成功（即`S[i] == P[j]`），都令`i++，j++`，继续匹配下一个字符；
>  3. 如果`j != -1`，且当前字符匹配失败（即`S[i] != P[j]`），则令` i `不变，`j = next[j]`。此举意味着失配时，模式串`P`相对于文本串`S`向右移动了`j - next [j]` 位。
>
> http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html
>
> https://segmentfault.com/a/1190000016331984
>
>

>```java
>【笔试前必备基础】将按空格、逗号或者分号隔开的字符串按字典序的顺序或者按逆字典序的顺序进行排列后输出。注意已知行数和未知行数的区别。此处分享一个用java编程可能会遇到的问题：
>如果输入的数据有三行，第一行是整数，第二行和第三行都是字符串，java中的Scanner类在nextInt()后输入的nextLine()无效。我相信很多人听不懂，举个代码给大家解释下。
>解决方法1：朴实无华的加上一个换行
>Scanner sc = new Scanner(System.in);
>int N = sc.nextInt();
>sc.nextLine(); //			如果就是不加这一个换行就是会出现bug呗 在这里哈呢
>String s1 = sc.nextLine();
>String s2 = sc.nextLine();
>s1 = s1.replaceAll(" ", "");
>s2 = s2.replaceAll(" ", "");
>```



## [ 重复的子字符串](https://leetcode-cn.com/problems/repeated-substring-pattern/)

## [实现 strStr() Kmp](https://leetcode-cn.com/problems/implement-strstr/)

>1. kmp算法流程在最上边
>2. 要知道前缀和后缀 
>3. 求next数组
>4. 模式匹配  `j=next[j]` 分三种情况： 1.相等 2.不等 3.走完了    i  j 就是while循环就是一定要套死呗 在这里哈呢

## [最短回文串](https://leetcode-cn.com/problems/shortest-palindrome/)



# ==压缩和解码->DFS==

## [字符串压缩](https://leetcode-cn.com/problems/compress-string-lcci/)

>1. 没啥难度 双指针遍历就是可以了呢



## [压缩字符串](https://leetcode-cn.com/problems/string-compression/)



## [字符串解码  ](https://leetcode-cn.com/problems/decode-string/)

>1. 这个点就是不会了呗 在这里哈呢





## ()()()  (()) == 2*2*2*3 笔试

>```java
>private static int dfs(String s) {
>   int len = s.length();
>   if (len <= 2) return len;
>   int res = 1;
>   Stack<Character> stack = new Stack<>();
>   stack.push('(');
>   int j = 0;
>   for (int i = 1; i < len; i++) {
>       if (s.charAt(i) == '(') stack.push('(');
>       else stack.pop();
>       if (stack.isEmpty()) {
>           if (i - j + 1 == len) {
>               return dfs(s.substring(1, 1 + i - j - 1)) + 1;  //((()))
>           }
>           res = res * dfs(s.substring(j, j + i - j + 1));
>           j = i + 1;
>       }
>   }
>   return res;
>}
>```





##  计算箱子个数  猿辅导笔试

>```java
>[][[][][]2]3  计算箱子个数  4 * 3 +3 +1 ==16   栈加递归
>public class Main {
>public static void main(String[] args) {
> Scanner in = new Scanner(System.in);
> String s = in.nextLine();
> System.out.println(getRes(s));
> //[][[][][]2]3  16
> //[][][[[]3[]2]2]2  28
>}
>
>public static int getRes(String s) {
> Stack<Integer> stack = new Stack<>();
> char[] arr = s.toCharArray();
> for (int i = 0; i < arr.length; i++) {
>     if (arr[i] == '[') {
>         stack.push(0);
>     } else {
>         if (stack.peek() == 0) {
>             int t = 0;
>             while (i + 1 < arr.length && arr[i + 1] != '[' && arr[i + 1] != ']') {
>                 i++;
>                 t = t * 10 + Integer.parseInt(String.valueOf(arr[i]));
>             }
>             if (t == 0) t = 1;
>             stack.pop();
>             stack.add(t);
>         } else {
>             int inScore = 0;
>             while (stack.peek() != 0) {
>                 inScore += stack.peek();
>                 stack.pop();
>             }
>             stack.pop();
>             int t = 0;
>             while (i + 1 < arr.length && arr[i + 1] != '[' && arr[i + 1] != ']') {
>                 i++;
>                 t = t * 10 + Integer.parseInt(String.valueOf(arr[i]));
>             }
>             stack.add((inScore + 1) * t);
>         }
>     }
> }
> int res = 0;
> while (!stack.empty()) {
>     res += stack.pop();
> }
> return res;
>}
>}
>```
>
>
>
>

# ==---------------------------------------------------------------单调栈==

## [数组判断是否为二叉搜索树后序遍历](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

## [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

## [最大矩形](https://leetcode-cn.com/problems/maximal-rectangle/)

## [每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

## [股票价格跨度](https://leetcode-cn.com/problems/online-stock-span/)

## [下一个更大元素 I](https://leetcode-cn.com/problems/next-greater-element-i/)

## [下一个更大元素 II](https://leetcode-cn.com/problems/next-greater-element-ii/)



## [去除重复字母](https://leetcode-cn.com/problems/remove-duplicate-letters/)

## [移掉K位数字](https://leetcode-cn.com/problems/remove-k-digits/)

## [子数组的最小值之和](https://leetcode-cn.com/problems/sum-of-subarray-minimums/)

# ==---------------------------------------------------------------栈与队列==



## [用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

## [用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

## [一个数组实现三个栈](https://leetcode-cn.com/problems/three-in-one-lcci/)

## 用循环数组实现队列

>```java
>public class QueueArray {
>
>private Object[] array;
>private int tail;   //队列下标
>private int front;  //队首下标
>private int len;
>
>public QueueArray(int size) {
>array = new Object[size];
>tail = 0;
>front = 0;
>size = len;
>}
>
>public boolean add(Object obj) {
>
>if (((tail + 1) & len) == front) return false;  //代表队列满了
>array[tail] = obj;
>tail = (tail + 1) % len;
>return true;
>}
>
>
>public Object remove() {
>if (front == tail) return null;  //队列是空的
>Object obj = array[front];
>front = (front + 1) % len;
>return obj;
>}
>}
>```





## [用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

>```xml
>用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
>输入：
>["CQueue","appendTail","deleteHead","deleteHead"]
>[[],[3],[],[]]
>输出：[null,null,3,-1]
>
>输入：
>["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
>[[],[],[5],[2],[],[]]
>输出：[null,-1,null,null,5,2]
>```
>
>**队列的特性：尾部删除元素 队列头部删除元素呢 这里边就是顺序别乱了**
>
>```java
>class CQueue {
>
>//利用两个栈实现队列呗 在这里哈呢
>private Stack<Integer> stack1;
>private Stack<Integer> stack2;
>
>public CQueue() {
>stack1=new Stack<>();
>stack2=new Stack<>();
>}
>
>public void appendTail(int value) {
>stack1.push(value);
>}
>
>//题目的意思就是 2栈不为空就重2栈里边取  如果为空就重1栈里边取 如果1栈为null 返回就是-1
>public int deleteHead() {
>if (stack2.isEmpty()) {
>  if (stack1.isEmpty())
>      return -1;
>  while (!stack1.isEmpty()) {
>      stack2.push(stack1.pop());
>  }
>}
>return stack2.pop();
>}
>}
>```



## [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)



## 猿辅导字符串解析

>```xml
>[][[][][]2]3  计算箱子个数  4 * 3 +3 +1 ==16   栈加递归
>```
>
>```java
>public class Main {
>public static void main(String[] args) {
>Scanner in = new Scanner(System.in);
>String s = in.nextLine();
>System.out.println(getRes(s));
>//[][[][][]2]3  16
>//[][][[[]3[]2]2]2  28
>}
>
>public static int getRes(String s) {
>Stack<Integer> stack = new Stack<>();
>char[] arr = s.toCharArray();
>for (int i = 0; i < arr.length; i++) {
>  if (arr[i] == '[') {
>      stack.push(0);
>  } else {
>      if (stack.peek() == 0) {
>          int t = 0;
>          while (i + 1 < arr.length && arr[i + 1] != '[' && arr[i + 1] != ']') {
>              i++;
>              t = t * 10 + Integer.parseInt(String.valueOf(arr[i]));
>          }
>          if (t == 0) t = 1;
>          stack.pop();
>          stack.add(t);
>      } else {
>          int inScore = 0;
>          while (stack.peek() != 0) {
>              inScore += stack.peek();
>              stack.pop();
>          }
>          stack.pop();
>          int t = 0;
>          while (i + 1 < arr.length && arr[i + 1] != '[' && arr[i + 1] != ']') {
>              i++;
>              t = t * 10 + Integer.parseInt(String.valueOf(arr[i]));
>          }
>          stack.add((inScore + 1) * t);
>      }
>  }
>}
>int res = 0;
>while (!stack.empty()) {
>  res += stack.pop();
>}
>return res;
>}
>}
>```





## [移掉 K 位数字](https://leetcode-cn.com/problems/remove-k-digits/)

>```
>输入：num = "1432219", k = 3
>输出："1219"
>解释：移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219 。
>```
>
>思路：  贪心加栈的思路  如果遇到前边比后边大的我们就是`pop()`出去  在考虑两个特殊情况
>
>1. `while(!stack.isEmpty() && k>0 && number<stack.peek())` 进行pop操作
>2. 如果当前元素不等于0我们进栈  如果等于0且栈不为空我们进栈
>3. 如果等于0 且栈为空  我们就是不添加
>4. 最后 判断是否这个序列一直是递增的 我们删除后边的元素就是可以
>5. 再者判断最后结果是否为0呢 在这里哈呢
>
>-----
>
>时间复杂度： O(N)
>
>空间复杂度： O(1)





## [最小栈](https://leetcode-cn.com/problems/min-stack/)

>这里边就是最小栈 我们就是不能就是使用临时变量来求解呗。
>
>一共有两个思路：
>
>1. 利用一个栈 同时添加当前元素  并且添加最小元素 
>2. 两用两个栈实现
>
>```java
>//每次入栈2个元素，一个是入栈的元素本身，一个是当前栈元素的最小值    如：入栈序列为2-3-1，则入栈后栈中元素序列为：2-2-3-2-1-1 
>public MinStack() {
>  stack = new Stack<Integer>();
>}
>
>public void push(int x) {
>  if(stack.isEmpty()){
>      stack.push(x);
>      stack.push(x);
>  }else{
>      int tmp = stack.peek();
>      stack.push(x);
>      if(tmp<x){
>          stack.push(tmp);
>      }else{
>          stack.push(x);
>      }
>  }
>}
>
>public void pop() {
>  stack.pop();
>  stack.pop();
>}
>
>public int top() {
>  return stack.get(stack.size()-2);
>}
>
>public int getMin() {
>  return stack.peek();
>}
>```





# ==-------------------------------------------------------------------hash哈希==

## [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

>1. 思路： 拿出来单词进行排序  之后放进`HashMap`里边呗 就是哈呢
>2. 返回时候就是在新建一个呗



## [单词规律](https://leetcode-cn.com/problems/word-pattern/)

>1. 这个就是利用`HashMap来计数`  分几种情况看是否存在就是可以了呢 
>2. 把一些就是边界条件就是考虑好了呢 在这里含额

## [存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

## [存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

## [寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)

## [数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

## [两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

## [两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

# ==----------------------------------------------------------智力题、大数进制==



## [分糖果](https://leetcode-cn.com/problems/distribute-candies/)

## [扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

## 打印2-100的质数

>```java
>import java.util.ArrayList;
>
>public class Main {
>public static void main(String[] args) {
>   for (int i = 2; i <= 100; i++) {
>       if (isPrime(i)){
>           System.out.print(" " + i);
>       }
>   }
>}
>// 判断是否为素数的方法
>public static boolean isPrime (int num) {
>   for (int i = 2 ; i <= Math.sqrt(num);i++) {
>       if (num % i == 0){
>           return false;
>       }
>   }
>   return true;
>}
>}
>```



## [整数反转](https://leetcode-cn.com/problems/reverse-integer/)

>```xml
>123-->321
>```
>
>跟下边就是回文数字思路差不多呢在这里





## [回文数](https://leetcode-cn.com/problems/palindrome-number/)

>```
>输入：x = 121
>输出：true
>```
>
>思路：
>
>1. 如果直接就是转化为字符串 那么会存在空间复杂度
>2. 计算反转一般的数字  判断是否是相等呢在这里哈呢  分奇数和偶数
>
>```java
>  public boolean isPalindrome(int x) {
>       // 特殊情况：
>       // 如上所述，当 x < 0 时，x 不是回文数。
>       // 同样地，如果数字的最后一位是 0，为了使该数字为回文，
>       // 则其第一位数字也应该是 0
>       // 只有 0 满足这一属性
>       if (x < 0 || (x % 10 == 0 && x != 0)) {
>           return false;
>       }
>
>       int revertedNumber = 0;
>       while (x > revertedNumber) {
>           revertedNumber = revertedNumber * 10 + x % 10;
>           x /= 10;
>       }
>
>       // 当数字长度为奇数时，我们可以通过 revertedNumber/10 去除处于中位的数字。
>       // 例如，当输入为 12321 时，在 while 循环的末尾我们可以得到 x = 12，revertedNumber = 123，
>       // 由于处于中位的数字不影响回文（它总是与自己相等），所以我们可以简单地将其去除。
>       return x == revertedNumber || x == revertedNumber / 10;
>   }
>```
>
>时间复杂度：O(logn)







## [剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)





## [数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

>```xml
>输入：x = 2.00000, n = 10
>输出：1024.00000
>```



## [x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

>```xml
>输入：x = 4
>输出：2
>```



## [打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)





## [1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)



##  [字符串相加](https://leetcode-cn.com/problems/add-strings/)

## 数组中左边最大、右边最小的元素

>```
>//输入：[2, 3, 1, 8, 9, 20, 12]
>//输出：3, 4
>//解释：数组中 8, 9 满足题目要求，他们的索引分别是 3、4
>```
>
>思路： 1. 要求时间复杂度 O(N)  我们在这里就是该怎么办呗 
>
> 		 2. 就是再新建立两个数组 一个表示当前元素左边最大值  一个表示当前元素右边最大值呗
> 	 	 3. 这种做法就是典型的时间换取空间被  
>
>```java
>public static List<Integer> find(int[] nums) {
>      //找到左边数字比较当前数字小 右边数字比当前数字大的两个数组呗
>      //这种就是进行时间上的优化 我们就是可以使用空间进行优化呗 在这里哈呢
>      int len = nums.length;
>      int[] left_max = new int[len];          //[0,i)     最大的      并且在这里边数组需要初始值 最小值呢
>      int[] right_min = new int[len];         //(i,len-1] 中最下的    在这里数组需要初始值最大值呢 在这里哈呢
>      Arrays.fill(left_max, Integer.MIN_VALUE);
>      Arrays.fill(right_min, Integer.MAX_VALUE);
>      for (int i = 1; i < len; i++) {
>          left_max[i] = Math.max(left_max[i - 1], nums[i - 1]);
>      }
>      for (int i = len - 2; i >= 0; i--) {
>          right_min[i] = Math.min(nums[i + 1], right_min[i + 1]);  //后续遍历 在这里我们找到右边最小值呗
>      }
>      List<Integer> list = new ArrayList<>();
>      for (int i = 0; i < len; i++) {
>          if (left_max[i] < nums[i] && nums[i] < right_min[i]) {
>              list.add(i);
>          }
>      }
>      return list;
>  }
>```



## [用 Rand7() 实现 Rand10()](https://leetcode-cn.com/problems/implement-rand10-using-rand7/)

>1. 关键点就是怎么实现正太分布  首先rand7*rand7  生成1--49 不符合正太分布
>2. (Rand7-1)*7  + rand7 这里边就是符合正太分布  1--49 概率我们就是1/49呢 这里边就是大于40我们就是舍弃呢 
>3. Res%10 在这里就是可以了呢  
>
>-----
>
>上述是一种实现方式
>
>```java
>      //思路：使用ran7在【0，6】直接选一个数 使用ran7在【0，5】之间选一个数
>        int a=rand7();int b=rand7();
>        while(a==7) a=rand7();	  	//a不能为7 必须为【0，6】这样才能保证奇偶都是1/2概率
>        while(b>5) b=rand7();		    //b不能为5以上 因为一会可能要加5
>        return ((a&1)==0?0:5)+b;    //判断a奇偶性1/2 * b取值【0，5】之间1/5=1/10
>```











# ==--------------------------------------------------------------------数据结构==

## [LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/)

>**LRU** 是 Least Recently Used 的缩写，这种算法认为最近使用的数据是热门数据，下一次很大概率将会再次被使用。而最近很少被使用的数据，很大概率下一次不再用到。当缓存容量的满时候，优先淘汰最近很少使用的数据。
>
>- 新数据直接插入到列表头部
>- 缓存数据被命中，将数据移动到列表头部
>- 缓存已满的时候，移除列表尾部数据。
>
>首选选用数据结构： 选双向链表删除头尾节点实际复杂度是O(1)
>
>​									散列表存储节点，获取节点的复杂度将会降低为 O(1)
>
><img src="http://www.justdojava.com/assets/images/2019/java/image_andyxh/20191020/LRU-185af50f.png" alt="img" style="zoom:67%;" />
>
>散列表中的value对应的是双向链表节点  
>
>同时双向链表中也要存放 `key value`  定义的时候加四个节点呗 在这里哈呢
>
>-----



## LFU

>1. **LRU(Least Recently Used)**最近最少使用算法，它是根据时间维度来选择将要淘汰的元素，即删除掉最长时间没被访问的元素。
>2. **LFU(Least Frequently Used)**最不经常使用算法，它是根据频率维度来选择将要淘汰的元素，即删除访问频率最低的元素。如果两个元素的访问频率相同，则淘汰最久没被访问的元素。也就是说LFU淘汰的时候会选择两个维度，先比较频率，选择访问频率最小的元素；如果频率相同，则按时间维度淘汰掉最久远的那个元素。
>   
>
>https://blog.csdn.net/hixiaoxiaoniao/article/details/109845322   
>
>

## LRU+TTL 缓存  GO语言实现

>设计：节点存放时间  
>
>1. Add操作： 先判断是否存在节点 存在替换移动到链表前头 --> 在判断是否超过缓存容量--->  移除末尾元素
>2. Get操作： 先判断是否存在 如果存在判断是否过期-->过期就是删除 
>
>```go
>package lru
>
>import (
>	"container/list"
>	"sync"
>	"time"
>)
>//缓存接口 
>type Cache interface {
>	Add(key, value interface{}, expiresAt time.Time)
>	Get(key interface{}) (interface{}, bool)
>	Remove(key interface{})
>	Len() int
>}
>
>// 缓存接口实现类
>type cache struct {
>	size  int
>	lru   *list.List
>	items map[interface{}]*list.Element
>}
>
>// 定义节点
>type entry struct {
>	key       interface{}
>	value     interface{}
>	expiresAt time.Time
>}
>
>// 无锁的缓存
>func NewUnlocked(size int) Cache {
>	if size <= 0 {
>		panic("inmem: must provide a positive size")
>	}
>	return &cache{
>		size:  size,
>		lru:   list.New(),
>		items: make(map[interface{}]*list.Element),
>	}
>}
>
>func (c *cache) Add(key, value interface{}, expiresAt time.Time) {
>	if ent, ok := c.items[key]; ok {
>		// update existing entry
>		c.lru.MoveToFront(ent)
>		v := ent.Value.(*entry)
>		v.value = value
>		v.expiresAt = expiresAt
>		return
>	}
>
>	// add new entry
>	c.items[key] = c.lru.PushFront(&entry{
>		key:       key,
>		value:     value,
>		expiresAt: expiresAt,
>	})
>
>	// remove oldest
>	if c.lru.Len() > c.size {
>		ent := c.lru.Back()
>		if ent != nil {
>			c.removeElement(ent)
>		}
>	}
>}
>
>func (c *cache) Get(key interface{}) (interface{}, bool) {
>	if ent, ok := c.items[key]; ok {
>		v := ent.Value.(*entry)
>
>		if v.expiresAt.After(time.Now()) {
>			// found good entry
>			c.lru.MoveToFront(ent)
>			return v.value, true
>		}
>
>		// ttl expired
>		c.removeElement(ent)
>	}
>	return nil, false
>}
>
>func (c *cache) Remove(key interface{}) {
>	if ent, ok := c.items[key]; ok {
>		c.removeElement(ent)
>	}
>}
>
>func (c *cache) Len() int {
>	return c.lru.Len()
>}
>
>// removeElement is used to remove a given list element from the cache
>func (c *cache) removeElement(e *list.Element) {
>	c.lru.Remove(e)
>	kv := e.Value.(*entry)
>	delete(c.items, kv.key)
>}
>
>// 设计带有锁的缓存  就是在原缓存的基础上加一个Lock锁即使可以了呢
>type lockedCache struct {
>	c cache
>	m sync.Mutex
>}
>
>// NewLocked constructs a new Cache of the given size that is safe for
>// concurrent use. If will panic if size is not a positive integer.
>func NewLocked(size int) Cache {
>	if size <= 0 {
>		panic("inmem: must provide a positive size")
>	}
>	return &lockedCache{
>		c: cache{
>			size:  size,
>			lru:   list.New(),
>			items: make(map[interface{}]*list.Element),
>		},
>	}
>}
>
>func (l *lockedCache) Add(key, value interface{}, expiresAt time.Time) {
>	l.m.Lock()
>	l.c.Add(key, value, expiresAt)
>	l.m.Unlock()
>}
>
>func (l *lockedCache) Get(key interface{}) (interface{}, bool) {
>	l.m.Lock()
>	v, f := l.c.Get(key)
>	l.m.Unlock()
>	return v, f
>}
>
>func (l *lockedCache) Remove(key interface{}) {
>	l.m.Lock()
>	l.c.Remove(key)
>	l.m.Unlock()
>}
>
>func (l *lockedCache) Len() int {
>	l.m.Lock()
>	c := l.c.Len()
>	l.m.Unlock()
>	return c
>}
>```







## bitmap位图 int实现

>```java
>public class BitMap {
>/**
>    * 如何确定用来存放数据的位图数组bitmap的大小？以及每个数据在bitmap中的位置？
>    * 如何对一个int类型的32为bit的某一个bit进行赋值操作？
>    * 如何对一个int类型的32为bit的某一个bit进行读取操作？
>    * 如何判重？
>    * 如何根据bitmap恢复原始数据？
>    */
>   private int[] bitmap;
>   public BitMap(int maxValue) {
>       int size = maxValue / 32 + 1;       //  bitmap 数组大小呗
>       bitmap = new int[size];
>       this.maxValue = maxValue;
>   }
>   public List<Integer> repeatNumList = new ArrayList<>();
>   public List<Integer> noExistNumList = new ArrayList<>();
>   private int maxValue;
>
>   //添加元素 并判断是否重复呗 在这里哈呢
>   public void add(int[] nums) {
>       for (int i = 0; i < nums.length; i++) {
>           int value = nums[i];
>           int index = value / 32;             //元素位于数组下标位置
>           int offset = value % 32 - 1;        //一个 int类型就是四个字节 32位二进制
>           int temp = bitmap[index];
>           bitmap[index] = bitmap[index] | 1 << offset;  //1<<offset即为value的bitmap的位置，与目前有的值进行或操作进行合并
>           if (temp == bitmap[index]) {
>               //这里边就是代表重复了  因为如果先前为0 现在为1 不会重复  如果先前就是为1 现在也为1 在这里就是重复了呢
>               repeatNumList.add(value);
>           }
>       }
>   }
>   public List<Integer> getRepeatNumList() {
>       return repeatNumList;
>   }
>   //遍历寻找 确实的元素呗  找出不存在的元素
>   public List<Integer> findLoseNum() {
>       int len = bitmap.length;
>       for (int i = 0; i < len; i++) {
>           //一个 int 类型就是32个字节
>           int num = bitmap[i];
>           for (int j = 0; j < 32; j++) {
>               boolean isExist = ((num >> j) & 0x01) == 0x01;    //如果为1 就是代表当前元素存在
>               if (!isExist) {
>                   //找到那个缺失的数字呗
>                   int loss = i * 32 + j + 1;
>                   if (loss < maxValue) {
>                       noExistNumList.add(loss);
>                   }
>               }
>           }
>       }
>       return noExistNumList;
>   }
>
>   public static void main(String[] args) {
>       BitMap whig = new BitMap(100);  // 找 1到100之中重复的数字 和 不存在的数字
>       int[] nums = {1, 1, 3, 4, 6, 7, 8, 9, 22, 44, 55, 99, 100, 100};
>       whig.add(nums);
>       System.out.println(whig.getRepeatNumList());
>       System.out.println(whig.findLoseNum());
>   }
>}
>```







## [Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

>前缀树  数据结构 挺难 但是还需要场景应用 在这里哈呢

>#### [单词搜索 II](https://leetcode-cn.com/problems/word-search-ii/)https://leetcode-cn.com/problems/word-search-ii/)
>
>#### [添加与搜索单词 - 数据结构设计](https://leetcode-cn.com/problems/design-add-and-search-words-data-structure/)
>
>#### [回文对](https://leetcode-cn.com/problems/palindrome-pairs/)
>
>#### [数组中两个数的最大异或值](https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/)
>
>#### [连接词](https://leetcode-cn.com/problems/concatenated-words/)
>
>#### [优美的排列 II](https://leetcode-cn.com/problems/beautiful-arrangement-ii/)
>
>#### [前缀和后缀搜索](https://leetcode-cn.com/problems/prefix-and-suffix-search/)
>
>#### [驼峰式匹配](https://leetcode-cn.com/problems/camelcase-matching/)



## 二叉树、搜索树、AVL、B+数、红黑树定义

>从数据结构的角度来讲，很大程度上是因为当遇到实际问题中那种既需要多次查找又需要多次更改的数据的时候（比如数据库），这个时候其实数组和链表都是不合适的，当然非要用也可以，但是从时间和空间复杂度上来讲都没有比较好的解决这个问题。
>
>##### 2. 二叉树
>
>二叉树指的是每个节点最多只能有两个子树的有序树。
>通常左边的子树被称作“左子树”(left subtree)，右边的子树被称为“右子树”(right subtree).由此可见，二叉树依然是树，它是一种特殊的树。
>二叉树的每个节点最多只有来两颗树(不存在度大于2的节点)，二叉树的子树有左，右之分，次序不能颠倒。
>树和二叉树的两个重要区别如下：
>
>- 树中节点的最大度数没有限制，而二叉树节点的最大度数为2，也就是说，二叉树是节点的最大度数为2的树。
>- 无序树的节点无左右之分，而二叉树的节点有左，右之分，也就是说，二叉树是有序树。
>
>-----
>
>
>
>##### 3. 二叉搜索树（二叉排序树，二叉查找树）
>
>二叉查找树（Binary Search Tree），（又：[二叉搜索树](https://baike.baidu.com/item/二叉搜索树)，二叉排序树）它或者是一棵空树，或者是具有下列性质的[二叉树](https://baike.baidu.com/item/二叉树)：
>
>- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
>- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
>- 它的左、右子树也分别为[二叉排序树](https://baike.baidu.com/item/二叉排序树)。
>
>![img](https:////upload-images.jianshu.io/upload_images/4941834-f2234909e241428d.png?imageMogr2/auto-orient/strip|imageView2/2/w/777/format/webp)
>
>二叉查找树
>
>##### 4. 平衡二叉搜索树（AVL树）
>
>平衡二叉搜索树（Self-balancing binary search tree）又被称为AVL树（有别于AVL算法），且具有以下性质：
>
>- 它是一 棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。
>
>平衡二叉树的常用实现方法有[红黑树](https://baike.baidu.com/item/红黑树)、[AVL](https://baike.baidu.com/item/AVL/7543015)、[替罪羊树](https://baike.baidu.com/item/替罪羊树)、[Treap](https://baike.baidu.com/item/Treap)、[伸展树](https://baike.baidu.com/item/伸展树)等。 最小二叉平衡树的节点的公式如下 F(n)=F(n-1)+F(n-2)+1 这个类似于一个递归的[数列](https://baike.baidu.com/item/数列)，可以参考Fibonacci(斐波那契)数列，1是根节点，F(n-1)是左子树的节点数量，F(n-2)是右子树的节点数量。
>
>[平衡二叉树打破平衡的调整----AVL 平衡二叉树旋转方法](https://blog.csdn.net/wanghanlincsdn/article/details/61208273)
>
>##### 5. B- 树
>
>1970年，R.Bayer和E.mccreight提出了一种适用于外查找的[树](https://baike.baidu.com/item/树)，它是一种平衡的多叉树，称为B树（或B-树、B_树）。**敲黑板，绝不能称之为B减树，会被笑话的。**
>
>一棵m阶B树(balanced tree of order m)是一棵平衡的m路搜索树。它或者是空树，或者是满足下列性质的树：
>
>- 1.根结点至少有两个子女；
>- 2、每个非根节点包含 k-1个元素和k个孩子，其中m/2 <= k <= m；
>- 4、所有的叶子结点都位于同一层。
>- 5.每个节点中的元素从小到大排列，节点当中k-1个元素正好是k个孩子包含的元素的值域分划
>
>![img](https:////upload-images.jianshu.io/upload_images/4941834-35f7fecf816f38da.png?imageMogr2/auto-orient/strip|imageView2/2/w/587/format/webp)
>
>B树，注意到卫星数据在所有节点元素中都带
>
>**B-树的应用：**
>
>- 文件系统
>- 部分数据库如 MengoDB 的索引
>
>##### 6. B+ 树
>
>B+树是 B树的变体，有着比B树更高的查询性能
>一个m阶的B+树具有如下几个特征：
>
>1.有k个子树的中间节点包含有k个元素（B树中是k-1个元素），每个元素不保存数据，只用来索引，所有数据都保存在叶子节点。
>
>2.所有的叶子结点中包含了全部元素的信息，及指向含这些元素记录的指针，且叶子结点本身依关键字的大小自小而大顺序链接。
>
>3.所有的中间节点元素都同时存在于子节点，在子节点元素中是最大（或最小）元素。
>
>
>
>![img](https:////upload-images.jianshu.io/upload_images/4941834-91b9729b186b0397.png?imageMogr2/auto-orient/strip|imageView2/2/w/591/format/webp)
>
>B+树
>
>在数据库的聚集索引（Clustered Index）中，叶子节点直接包含卫星数据。在非聚集索引（NonClustered Index）中，叶子节点带有指向卫星数据的指针。
>
>B+树的结构设计带来的好处：
>非叶子节点不包含卫星数据，使得B+树的身形更加矮胖，查询IO次数更少；
>B+树上的查询都是遍历到根节点，性能较B-树要稳定；
>范围查询比B-树方便，找到下界后沿链表往后遍历即可。
>
>##### 7. 红黑树
>
>红黑树是平衡二叉查找树的一种实现，但是并没有追求绝对的平衡。
>红黑树在符合二叉查找树的特征之外，还具有以下的附加特征：
>
>- 1.节点是红色或黑色。
>- 2.根节点是黑色。
>- 3.每个叶子节点都是黑色的空节点（NIL节点）。
>- 4 每个红色节点的两个子节点都是黑色。(从每个叶子到根的所有路径上不能有两个连续的红色节点)
>- 5.从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。
>
>![img](https:////upload-images.jianshu.io/upload_images/4941834-b95dae25a58aa1a3.png?imageMogr2/auto-orient/strip|imageView2/2/w/689/format/webp)
>
>

>- 二叉树 插入 删除操作
>
>- 二叉搜索树
>
>- [二叉树](https://www.nowcoder.com/jump/super-jump/word?word=二叉树)和B树的区别
>
> B树和B+树的区别
>
>- [红黑树](https://www.nowcoder.com/jump/super-jump/word?word=红黑树)和[平衡二叉树](https://www.nowcoder.com/jump/super-jump/word?word=平衡二叉树)的区别
>- 满二叉树 AVL树

# ==---------------------------------------------------------------多线程 JAVA==

# 两个线程顺序输出

>https://developer.aliyun.com/article/776793  		总结的比较全面
>
>```xml
>1. 三个线程分别打印 A，B，C，要求这三个线程一起运行，打印 n 次，输出形如“ABCABCABC....”的字符串
>2. 两个线程交替打印 0~100 的奇偶数
>3. 通过 N 个线程顺序循环打印从 0 至 100
>4. 多线程按顺序调用，A->B->C，AA 打印 5 次，BB 打印10 次，CC 打印 15 次，重复 10 次
>5. 用两个线程，一个输出字母，一个输出数字，交替输出 1A2B3C4D...26Z
>```
>
>
>
>两个线程顺序输出 有几种方法  哪个方法在这里就是最好的呢
>
>1. **join():**是Theard的方法，作用是调用线程需等待该join()线程执行完成后，才能继续用下运行
>2. `wait`和`notify` + `synchronized`方法 经典的就是生产者和消费者模式
>3. `Lock` 中方法
>4. `LockSupport.park( )`和 `LockSupport.unpark()`
>5. 

## 三个线程分别打印 A，B，C  ---->   使用 Lock

>我们以第一题为例：三个线程分别打印 A，B，C，要求这三个线程一起运行，打印 n 次，输出形如“ABCABCABC....”的字符串。
>
>思路：使用一个取模的判断逻辑 **C%M ==N**，题为 3 个线程，所以可以按取模结果编号：0、1、2，他们与 3 取模结果仍为本身，则执行打印逻辑。
>
>```java
>public class PrintABCUsingLock {
>
>    private int times; // 控制打印次数
>    private int state;   // 当前状态值：保证三个线程之间交替打印
>    private Lock lock = new ReentrantLock();
>
>    public PrintABCUsingLock(int times) {
>        this.times = times;
>    }
>
>    private void printLetter(String name, int targetNum) {
>        for (int i = 0; i < times; ) {
>            lock.lock();
>            if (state % 3 == targetNum) {
>                state++;
>                i++;
>                System.out.print(name);
>            }
>            lock.unlock();
>        }
>    }
>
>    public static void main(String[] args) {
>        PrintABCUsingLock loopThread = new PrintABCUsingLock(1);
>
>        new Thread(() -> {
>            loopThread.printLetter("B", 1);
>        }, "B").start();
>        
>        new Thread(() -> {
>            loopThread.printLetter("A", 0);
>        }, "A").start();
>        
>        new Thread(() -> {
>            loopThread.printLetter("C", 2);
>        }, "C").start();
>    }
>}
>```
>
>main 方法启动后，3 个线程会抢锁，但是 state 的初始值为 0，所以第一次执行 if 语句的内容只能是 **线程 A**，然后还在 for 循环之内，此时 `state = 1`，只有 **线程 B** 才满足 `1% 3 == 1`，所以第二个执行的是 B，同理只有 **线程 C** 才满足 `2% 3 == 2`，所以第三个执行的是 C，执行完 ABC 之后，才去执行第二次 for 循环，所以要把 i++ 写在 for 循环里边，不能写成 `for (int i = 0; i < times;i++)` 这样。



## 三个线程分别打印 A，B，C     ---->使用 wait和 notify

> join()，或者 wati/notify 这样的思路。算是比较传统且万能的解决方案。也有些面试官会要求不能使用这种方式。
>
>我们用对象监视器来实现，通过 `wait` 和 `notify()` 方法来实现等待、通知的逻辑，A 执行后，唤醒 B，B 执行后唤醒 C，C 执行后再唤醒 A，这样循环的等待、唤醒来达到目的。
>
>```java
>public class PrintABCUsingWaitNotify {
>
>    private int state;
>    private int times;
>    private static final Object LOCK = new Object();
>
>    public PrintABCUsingWaitNotify(int times) {
>        this.times = times;
>    }
>
>    public static void main(String[] args) {
>        PrintABCUsingWaitNotify printABC = new PrintABCUsingWaitNotify(10);
>        new Thread(() -> {
>            printABC.printLetter("A", 0);
>        }, "A").start();
>        new Thread(() -> {
>            printABC.printLetter("B", 1);
>        }, "B").start();
>        new Thread(() -> {
>            printABC.printLetter("C", 2);
>        }, "C").start();
>    }
>
>    private void printLetter(String name, int targetState) {
>        for (int i = 0; i < times; i++) {
>            synchronized (LOCK) {
>                while (state % 3 != targetState) {
>                    try {
>                        LOCK.wait();       //wait方法在这里会进行锁释放 `yield``sleep()`方法调用后不会释放锁。会进入等待队列
>                    } catch (InterruptedException e) {
>                        e.printStackTrace();
>                    }
>                }
>                state++;
>                System.out.print(name);
>                LOCK.notifyAll();
>            }
>        }
>    }
>}
>```



## 三个线程分别打印 A，B，C     ---->使用 Condition

>```xml
>Condition 中的 await() 方法相当于 Object 的 wait() 方法，Condition 中的 signal() 方法相当于Object 的 notify() 方法，Condition 中的 signalAll() 相当于 Object 的 notifyAll() 方法。
>
>不同的是，Object 中的 wait(),notify(),notifyAll()方法是和"同步锁"(synchronized关键字)捆绑使用的；而 Condition 是需要与"互斥锁"/"共享锁"捆绑使用的。
>```
>
>```java
>public class PrintABCUsingLockCondition {
>
>    private int times;
>    private int state;
>    private static Lock lock = new ReentrantLock();
>    private static Condition c1 = lock.newCondition();
>    private static Condition c2 = lock.newCondition();
>    private static Condition c3 = lock.newCondition();
>
>    public PrintABCUsingLockCondition(int times) {
>        this.times = times;
>    }
>
>    public static void main(String[] args) {
>        PrintABCUsingLockCondition print = new PrintABCUsingLockCondition(10);
>        new Thread(() -> {
>            print.printLetter("A", 0, c1, c2);
>        }, "A").start();
>        new Thread(() -> {
>            print.printLetter("B", 1, c2, c3);
>        }, "B").start();
>        new Thread(() -> {
>            print.printLetter("C", 2, c3, c1);
>        }, "C").start();
>    }
>
>    private void printLetter(String name, int targetState, Condition current, Condition next) {
>        for (int i = 0; i < times; ) {
>            lock.lock();
>            try {
>                while (state % 3 != targetState) {
>                    current.await();
>                }
>                state++;
>                i++;
>                System.out.print(name);
>                next.signal();
>            } catch (Exception e) {
>                e.printStackTrace();
>            } finally {
>                lock.unlock();
>            }
>        }
>    }
>}
>```
>
>使用 Lock 锁的多个 Condition 可以实现精准唤醒，所以碰到那种多个线程交替打印不同次数的题就比较容易想到，



## 三个线程分别打印 A，B，C  --->使用 Semaphore

>在信号量上我们定义两种操作： 信号量主要用于两个目的，一个是用于多个共享资源的互斥使用，另一个用于并发线程数的控制。
>
>1. acquire（获取） 当一个线程调用 acquire 操作时，它要么通过成功获取信号量（信号量减1），要么一直等下去，直到有线程释放信号量，或超时。
>2. release（释放）实际上会将信号量的值加1，然后唤醒等待的线程
>
>```java
>import java.util.concurrent.Semaphore;
>public class PrintABCUsingSemaphore {
>   private int times;
>   private static Semaphore semaphoreA = new Semaphore(1); // 只有A 初始信号量为1,第一次获取到的只能是A
>   private static Semaphore semaphoreB = new Semaphore(0);
>   private static Semaphore semaphoreC = new Semaphore(0);
>
>   public PrintABCUsingSemaphore(int times) {
>       this.times = times;
>   }
>
>   public static void main(String[] args) {
>       PrintABCUsingSemaphore printer = new PrintABCUsingSemaphore(1);
>       new Thread(() -> {
>           printer.print("A", semaphoreA, semaphoreB);
>       }, "A").start();
>
>       new Thread(() -> {
>           printer.print("B", semaphoreB, semaphoreC);
>       }, "B").start();
>
>       new Thread(() -> {
>           printer.print("C", semaphoreC, semaphoreA);
>       }, "C").start();
>   }
>
>   private void print(String name, Semaphore current, Semaphore next) {
>       for (int i = 0; i < times; i++) {
>           try {
>               System.out.println("111" + Thread.currentThread().getName());
>               current.acquire();  // A获取信号执行,A信号量减1,当A为0时将无法继续获得该信号量
>               System.out.print(name);
>               next.release();    // B释放信号，B信号量加1（初始为0），此时可以获取B信号量
>               System.out.println("222" + Thread.currentThread().getName());
>           } catch (InterruptedException e) {
>               e.printStackTrace();
>           }
>       }
>   }
>}
>```
>
>如果题目中是多个线程循环打印的话，一般使用信号量解决是效率较高的方案，上一个线程持有下一个线程的信号量，通过一个信号量数组将全部关联起来，这种方式不会存在浪费资源的情况。



## 三个线程分别打印 A，B，C  --->使用 LockSupport

>LockSupport 是 JDK 底层的基于 `sun.misc.Unsafe` 来实现的类，用来创建锁和其他同步工具类的基本线程阻塞原语。它的静态方法`unpark()`和`park()`可以分别实现阻塞当前线程和唤醒指定线程的效果，所以用它解决这样的问题会更容易一些。
>
>（在 AQS 中，就是通过调用 `LockSupport.park( )`和 `LockSupport.unpark()` 来实现线程的阻塞和唤醒的。
>
>```java
>public class PrintABCUsingLockSupport {
>
>    private static Thread threadA, threadB, threadC;
>
>    public static void main(String[] args) {
>        threadA = new Thread(() -> {
>            for (int i = 0; i < 10; i++) {
>                // 打印当前线程名称
>                System.out.print(Thread.currentThread().getName());
>                // 唤醒下一个线程
>                LockSupport.unpark(threadB);
>                // 当前线程阻塞
>                LockSupport.park();
>            }
>        }, "A");
>        threadB = new Thread(() -> {
>            for (int i = 0; i < 10; i++) {
>                // 先阻塞等待被唤醒
>                LockSupport.park();
>                System.out.print(Thread.currentThread().getName());
>                // 唤醒下一个线程
>                LockSupport.unpark(threadC);
>            }
>        }, "B");
>        threadC = new Thread(() -> {
>            for (int i = 0; i < 10; i++) {
>                // 先阻塞等待被唤醒
>                LockSupport.park();
>                System.out.print(Thread.currentThread().getName());
>                // 唤醒下一个线程
>                LockSupport.unpark(threadA);
>            }
>        }, "C");
>        threadA.start();
>        threadB.start();
>        threadC.start();
>    }
>}
>```





# 通过 N 个线程顺序循环打印从 0 至 100

>```java
>public class LoopPrinter {
>
>    private final static int THREAD_COUNT = 3;
>    static int result = 0;
>    static int maxNum = 10;
>
>    public static void main(String[] args) throws InterruptedException {
>        final Semaphore[] semaphores = new Semaphore[THREAD_COUNT];
>        for (int i = 0; i < THREAD_COUNT; i++) {
>            //非公平信号量，每个信号量初始计数都为1
>            semaphores[i] = new Semaphore(1);
>            if (i != THREAD_COUNT - 1) {
>                System.out.println(i+"==="+semaphores[i].getQueueLength());
>                //获取一个许可前线程将一直阻塞, for 循环之后只有 syncObjects[2] 没有被阻塞
>                semaphores[i].acquire();
>            }
>        }
>        for (int i = 0; i < THREAD_COUNT; i++) {
>            // 初次执行，上一个信号量是 syncObjects[2]
>            final Semaphore lastSemphore = i == 0 ? semaphores[THREAD_COUNT - 1] : semaphores[i - 1];
>            final Semaphore currentSemphore = semaphores[i];
>            final int index = i;
>             new Thread(() -> {
>                try {
>                    while (true) {
>                        // 初次执行，让第一个 for 循环没有阻塞的 syncObjects[2] 先获得令牌阻塞了
>                        lastSemphore.acquire();
>                        System.out.println("thread" + index + ": " + result++);
>                        if (result > maxNum) {
>                            System.exit(0);
>                        }
>                        // 释放当前的信号量，syncObjects[0] 信号量此时为 1，下次 for 循环中上一个信号量即为syncObjects[0]
>                        currentSemphore.release();
>                    }
>                } catch (Exception e) {
>                    e.printStackTrace();
>                }
>            }).start();
>        }
>    }
>```



# java线程实现死锁

>https://www.jianshu.com/p/0211fdd410ae
>
>- 方式一 线程之间持有互相对象的锁 导致死锁  这里边必须是两个共享资源以上
>
>```java
>public class Test {
>
>    public static Object a = new Object();
>    public static Object b = new Object();
>
>    public static void main(String[] args) {
>        new Thread(new LockA()).start();
>        new Thread(new LockB()).start();
>    }
>}
>class LockA implements Runnable {
>    @Override
>    public void run() {
>        System.out.println("LockA开始执行");
>        while (true) {                      
>            synchronized (Test.a) {
>                System.out.println("锁住a对象");
>                try {
>                    Thread.sleep(1000);
>                } catch (InterruptedException e) {
>                    e.printStackTrace();
>                }
>                synchronized (Test.b) {
>                    System.out.println("需要b资源才可以开始进行执行");
>                }
>            }
>        }
>    }
>}
>class LockB implements Runnable {
>    @Override
>    public void run() {
>        System.out.println("LockB开始执行");
>        while (true) {
>            synchronized (Test.b) {
>                System.out.println("锁住b对象");
>                try {
>                    Thread.sleep(1000);
>                } catch (InterruptedException e) {
>                    e.printStackTrace();
>                }
>                synchronized (Test.a) {
>                    System.out.println("需要a资源才可以继续工作");
>                }
>            }
>        }
>    }
>}
>```
>
>

# java实现读写锁

>```java
>public class ReadWriteLock {
>  /**
>   * 读锁持有个数
>   */
>  private int readCount = 0;
>  /**
>   * 写锁持有个数
>   */
>  private int writeCount = 0;
>
>  /**
>   * 获取读锁,读锁在写锁不存在的时候才能获取
>   */
>  public synchronized void lockRead() throws InterruptedException {
>    // 写锁存在,需要wait
>    while (writeCount > 0) {
>      wait();
>    }
>    readCount++;
>  }
>
>  /**
>   * 释放读锁
>   */
>  public synchronized void unlockRead() {
>    readCount--;
>    notifyAll();
>  }
>
>  /**
>   * 获取写锁,当读锁存在时需要wait.
>   */
>  public synchronized void lockWrite() throws InterruptedException {
>    // 先判断是否有写请求
>    while (writeCount > 0) {
>      wait();
>    }
>
>    // 此时已经不存在获取写锁的线程了,因此占坑,防止写锁饥饿
>    writeCount++;
>
>    // 读锁为0时获取写锁
>    while (readCount > 0) {
>      wait();
>    }
>  }
>
>  /**
>   * 释放读锁
>   */
>  public synchronized void unlockWrite() {
>    writeCount--;
>    notifyAll();
>  }
>}
>```



# ==------------------------------------------------------------------------------GO==

# 三个线程累加数字

>开启三个协程 累加数字到1000
>
>```go
>// 三个协程累加数字  重0累加到3000
>var num int = 0
>func main() {
>	mutex := &sync.Mutex{}
>	waitGroup := &sync.WaitGroup{}
>	for i := 0; i < 3; i++ {
>		waitGroup.Add(1)		//这里边就是先添加 不要在addNum里边添加 否则就是main函数执行完毕了
>		go addNum(mutex, waitGroup)
>	}
>	waitGroup.Wait()
>	fmt.Println(num)
>	fmt.Println("三个线程累加数字")
>}
>
>func addNum(mutex *sync.Mutex, waitGroup *sync.WaitGroup) {
>	for i := 0; i < 1000; i++ {
>		mutex.Lock()
>		num++
>		mutex.Unlock()
>	}
>	waitGroup.Done()
>	return
>}
>```
>
>这里边涉及知识点：---》 `sync.mutex  sync.WaitGroup`  

# 顺序打印A、B、C 100次

>- 使用 `sync`  以及 `int`变量
>
>```go
>var time int = 2
>var state int = 0
>func printString(str string, targetNum int, mutex *sync.Mutex, waitGroup *sync.WaitGroup) {
>	for i := 0; i < time; {
>		mutex.Lock()
>		if state%3 == targetNum {
>			state++ //以及这个state++
>			i++     //这里边i++是精髓呗 如果在这里就不是i++ 三个协程很快就是执行完毕了呢
>			fmt.Println(str)
>		}
>		mutex.Unlock()
>	}
>	waitGroup.Done()
>}
>func main() {
>	mutex := &sync.Mutex{}
>	waitGroup := &sync.WaitGroup{}
>	waitGroup.Add(3)
>	go printString("A", 0, mutex, waitGroup)
>	go printString("B", 1, mutex, waitGroup)
>	go printString("C", 2, mutex, waitGroup)
>	waitGroup.Wait()
>}
>```
>
>------
>
>- 使用`chan`来进行通信 
>
>```go
>func main() {
> group := &sync.WaitGroup{}
> chanA := make(chan struct{}, 1)   //后边必须要跟1 否则就是报错呢
> chanB := make(chan struct{}, 1)
> chanC := make(chan struct{}, 1)
> chanA <- struct{}{}
> group.Add(3)
> go printABC(chanA, chanB, group, "A")
> go printABC(chanB, chanC, group, "B")
> go printABC(chanC, chanA, group, "C")
> group.Wait()
>}
>
>// chan 来实现进程之间的通信呗
>func printABC(now chan struct{}, next chan struct{}, group *sync.WaitGroup, str string) {
> for i := 0; i < 2; i++ {
>    <-now								           //当前进行读
>    fmt.Println(str)
>    next <- struct{}{}						 //下一个进行写入
> }
> group.Done()
> return
>}
>```





# ==--------------------------------------------------------------------------场景提==

