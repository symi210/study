# Study

[TOC]

## A
### Algorithm
#### LeetCode
##### 10. 正则表达式匹配
```java
/**
 * LC10
 * 正则表达式匹配
 * 给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。
 *
 * '.' 匹配任意单个字符
 * '*' 匹配零个或多个前面的那一个元素
 * 所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。
 *
 * 说明:
 *
 * s 可能为空，且只包含从 a-z 的小写字母。
 * p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。
 * 示例 1:
 *
 * 输入:
 * s = "aa"
 * p = "a"
 * 输出: false
 * 解释: "a" 无法匹配 "aa" 整个字符串。
 *
 * 来源：力扣（LeetCode）
 * 链接：https://leetcode-cn.com/problems/regular-expression-matching
 * 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
 */
public class Solution {
	public static void main(String[] args) {
	    String[][] arr = {
	            {"", ""},
	            {"", "a*"},
	            {"aa", "a*"},
	            {"aa", ".*"},
	            {"ab", "c*a*b"},
	            {"a", ""},
	            {"", "a"},
	            {"", "."},
	            {"aa", "a"},
	    };
	    for (String[] item: arr) {
	        System.out.println(isMatch(item[0], item[1]));
	    }
	}
	public static boolean isMatch(String s, String p) {
		if (p.isEmpty()) {
			return s.isEmpty();
		}

		boolean firstMatch = (!s.isEmpty() && (s.charAt(0) == p.charAt(0) || p.charAt(0) == '.'));

		if (p.length() >= 2 && p.charAt(1) == '*') {
			return (firstMatch && isMatch(s.substring(1), p)) || isMatch(s, p.substring(2));
		} else {
			return firstMatch && isMatch(s.substring(1), p.substring(1));
		}
	}
}
```

##### 11. 盛最多水的容器
```java
/**
 * LC11
 * 盛最多水的容器
 * 给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
 *
 * 说明：你不能倾斜容器，且 n 的值至少为 2。
 *
 * 示例:
 * 输入: [1,8,6,2,5,4,8,3,7]
 * 输出: 49
 * 来源：力扣（LeetCode）
 * 链接：https://leetcode-cn.com/problems/container-with-most-water
 * 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
 */
 public class Solution {
 	public static void main(String[] args) {
 		int[][] arrs = {
                {1, 8, 6, 2, 5, 4, 8, 3, 7},
                {1, 8},
                {1, 8, 6},
                {1, 8, 6, 2},
                {1, 8, 6, 2, 5},
                {1, 8, 6, 2, 5, 4},
                {1, 8, 6, 2, 5, 4, 8},
                {1, 8, 6, 2, 5, 4, 8, 3}
        };
        for (int[] arr: arrs) {
            System.out.println(maxArea(arr));
        }
 	}

 	public static int maxArea(int[] height) {
 		int max = 0;
        int l = 0, r = height.length - 1;
        while (l < r) {
            max = Math.max(max, Math.min(height[l], height[r]) * (r - l));
            if (height[l] < height[r]) {
                l++;
            } else {
                r--;
            }
        }
        return max;
    }
 }
```

##### 15. 三数之和
```java
/**
 * LC15
 * 三数之和
 * 给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。
 *
 * 注意：答案中不可以包含重复的三元组。
 *
 *
 * 示例：
 *
 * 给定数组 nums = [-1, 0, 1, 2, -1, -4]，
 *
 * 满足要求的三元组集合为：
 * [
 *   [-1, 0, 1],
 *   [-1, -1, 2]
 * ]
 *
 * 来源：力扣（LeetCode）
 * 链接：https://leetcode-cn.com/problems/3sum
 * 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
 */
public class Solution {
    public static void main(String[] args) {
        int[][] arrs = {
                {-1, 0, 1, 2, -1, -4},
                {-2, 0, 0, 0, 2}
        };
        for (int[] arr: arrs) {
            System.out.println(threeSum(arr).toString());
        }
    }

    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length < 3) {
            return result;
        }

        Arrays.sort(nums);

        int second, third, sum;
        for (int first = 0; first < nums.length - 2; first++) {
            if (first == 0 || nums[first] > nums[first - 1]) {
                second = first + 1;
                third = nums.length - 1;
                while (second < third) {
                    sum = nums[first] + nums[second] + nums[third];
                    if (sum == 0) {
                        result.add(Arrays.asList(nums[first], nums[second], nums[third]));
                        second++;
                        third--;
                        while (second < third && nums[second] == nums[second - 1]) {
                            second++;
                        }
                        while (second < third && nums[third] == nums[third + 1]) {
                            third--;
                        }
                    } else if (sum < 0) {
                        second++;
                        while (second < third && nums[second] == nums[second - 1]) {
                            second++;
                        }
                    } else {
                        third--;
                        while (second < third && nums[third] == nums[third + 1]) {
                            third--;
                        }
                    }
                }
            }
        }
        return result;
    }
}
```

##### 17. 电话号码的字母组合
```java
/**
 * LC17
 * 电话号码的字母组合
 * 给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
 *
 * 给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
 *
 *
 * 示例:
 *
 * 输入："23"
 * 输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
 *
 * 来源：力扣（LeetCode）
 * 链接：https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number
 * 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
 */
public class LetterCombinations {
    public static void main(String[] args) {
        System.out.println(letterCombinations("23"));
        System.out.println(letterCombinations(""));
        System.out.println(letterCombinations("34"));
    }

    private static List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (!digits.matches("^[2-9]+$")) {
            return result;
        }

        Map<String, String> map = new HashMap<>();
        map.put("2", "abc");
        map.put("3", "def");
        map.put("4", "ghi");
        map.put("5", "jkl");
        map.put("6", "mno");
        map.put("7", "pqrs");
        map.put("8", "tuv");
        map.put("9", "wxyz");
        return combination(digits, 0, map);
    }

    private static List<String> combination(String digits, int index, Map<String, String> map) {
        List<String> result = new ArrayList<>();
        if (digits.length() <= index) {
            return result;
        }

        List<String> leftResult = combination(digits, index + 1, map);
        if (leftResult.size() == 0) {
            leftResult.add("");
        }
        String letter = map.get(String.valueOf(digits.charAt(index)));
        for (int i = 0; i < letter.length(); i++) {
            for (String item: leftResult) {
                result.add(letter.charAt(i) + item);
            }
        }
        return result;
    }
```

#### 几种常见的排序算法

#### 数组循环右移k位
-----

## D
### [Database](https://github.com/rasp210/study/blob/master/database)
##### [MySQL](https://github.com/rasp210/study/blob/master/database/mysql)
1. [Engine 引擎](https://github.com/rasp210/study/blob/master/database/mysql/engine.md)
2. [Index 索引](https://github.com/rasp210/study/blob/master/database/mysql/index.md)
3. [Transaction 事务](https://github.com/rasp210/study/blob/master/database/mysql/transaction.md)
4. [Explain](https://github.com/rasp210/study/blob/master/database/mysql/explain.md)

##### [Redis](https://github.com/rasp210/study/blob/master/database/redis)
##### [MongoDB](https://github.com/rasp210/study/blob/master/database/mongodb)
-----

### [Design Pattern](https://github.com/rasp210/study/blob/master/design-pattern)
##### [设计模式](https://github.com/rasp210/study/blob/master/design-pattern/design-pattern.md)
-----

### [Docker](https://github.com/rasp210/study/tree/master/git)
-----

## E
### [Exception](https://github.com/rasp210/study/blob/master/exceptions/exceptions.md)
遇到的各种异常/错误/问题等。
1. [Mac terminal ls 别名设置带颜色失败](https://github.com/rasp210/study/blob/master/exceptions/mac-alias-ls-color.md)

-----

## G
### [Git](https://github.com/rasp210/study/tree/master/git)
Git 是分布式版本控制系统的一种。客户端把仓库完整地镜像下来，这样，任何一处协同工作用的服务器发生故障，都可以通过任何一个镜像出来的本地仓库恢复。因为每一次的克隆操作，实际上都是一次代码仓库的完整备份。
1. [简介及配置](https://github.com/rasp210/study/tree/master/git/intro-config.md)
2. [命令](https://github.com/rasp210/study/tree/master/git/command.md)
3. [冲突解决](https://github.com/rasp210/study/tree/master/git/conflict.md)
-----

## J
### Java
#### 基础
##### 1. Java类加载机制？

##### 2. Exception和Error有什么区别？
```
Exception和Error都是继承自Throwable类，Java中只有Throwable类型的实例才可以被抛出或者捕获，它是异常处理机制的基本组成类型，体现了Java平台设计者对不同异常情况的分类。
Exception是程序正常运行过程中，可以预料的意外情况，可以并且应该被捕获，进行相应处理。
Error是指在正常情况下，不大可能出现的情况，绝大多数Error都会导致程序处于非正常、不可恢复状态，不便于也不需要捕获。
异常又可以分为可检查和不检查异常，可检查异常必须显示的进行捕获处理，这是编译期检查的一部分；不检查异常包括运行时异常和Error。
```

##### 3. final、finally和finalize有什么不同？
```
final可以用来修饰类、方法、变量，final类不可以被继承，final方法不可以被重写，final变量不可以被修改。
finally是java保证重要代码一定要被执行的一种机制，通常使用try-finally或try-catch-finally来进行类似资源关闭等操作。但是更推荐使用JDK7中try-with-resources语句来关闭资源。
finalize是java.lang.Object的一个方法，是保证对象在被垃圾回收前完成特定资源的回收，在JDK9中已经标记为deprecated。java目前逐步使用java.lang.ref.Cleaner来替换原有的finalize，Cleaner的实现利用了幻象引用，这是一种常见的post-mortem机制。
```

#### 虚拟机
##### 1. 常见的垃圾回收器
SerialGC
ParallelGC
CMS
G1
基本原理？
适用于什么样的工作负载？

##### 2. 诊断工具？
jmap
jstack
jconsole
jhsdb
jcmd

##### 3. java是解释执行还是编译执行
javac是将源码编译成字节码的.class文件
在运行时，JVM会通过类加载器加载字节码，解释或者编译执行
JDK8是解释和编译混合的一种模式(-Xmixed)
通常运行在server模式下的JVM，会进行上万次的调用，以收集足够的信息进行高效编译
client模式这个门限是1500次，适用于对启动速度敏感的应用
默认采用分层编译
AOT编译（Ahead Of Time Compililation）：直接将字节码编译成机器码，这样就避免了JIT预热等各方面的开销（JDK9）

##### 4. java应用启动参数
-Xint：JVM仅进行解释执行
-Xcomp：JVM仅进行编译执行，最大优化级别
JDK9
jaotc --output libHelloWorld.so HelloWorld.class
jaotc --output libjava.base.so --module java.base
java -XX:AOTLibrary=./libHelloWorld.so,./libjava.base.so HelloWorld

#### IO/NIO
#### 并发
#### 分布式
#### 安全
#### 性能
#### 范型
#### Lambda
#### 反射
-----
## L
### [Linux](https://github.com/rasp210/study/blob/master/linux)   
- [awk](https://github.com/rasp210/study/blob/master/linux/awk.md)     
- [ps](https://github.com/rasp210/study/blob/master/linux/ps.md)   
- [rpm](https://github.com/rasp210/study/blob/master/linux/rpm.md)   
- [sed](https://github.com/rasp210/study/blob/master/linux/sed.md)   
- [uniq](https://github.com/rasp210/study/blob/master/linux/uniq.md)
- [Shell特殊变量](https://github.com/rasp210/study/blob/master/linux/shell-special-variable.md)   

-----

## N
### [Network](https://github.com/rasp210/study/blob/master/network)

-----

## O
### [Operating System](https://github.com/rasp210/study/blob/master/os)

-----

## P
### [PHP](https://github.com/rasp210/study/blob/master/php)   
1. [PHP源码](https://github.com/rasp210/study/blob/master/php/source-code.md)   
2. [PHP框架](https://github.com/rasp210/study/blob/master/php/framework.md)   
3. [LNMP介绍](https://github.com/rasp210/study/blob/master/php/lnmp.md)     
-----

### [Python](https://github.com/rasp210/study/blob/master/python)

-----

## S
### [Security](https://github.com/rasp210/study/blob/master/security)

常见网络攻击，安全问题处理等。

-----

## T
### [Tool](https://github.com/rasp210/study/blob/master/tool)
Excel，Markdown等工具的使用。
1. [Excel](https://github.com/rasp210/study/blob/master/tool/excel.md)
-----
