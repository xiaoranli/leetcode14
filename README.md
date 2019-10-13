3、leetcode14. 最长公共前缀
==
解法一：水平扫描  
--
思路：
--
    想象数组的末尾有一个非常短的字符串，使用上述方法依旧会进行 S 次比较。优化这类情况的一种方法就是水平扫描。我们从前往后枚举字符串的每一列，先比较每个字符串相同列上的字符（即不同字符串相同下标的字符）然后再进行对下一列的比较。  
代码： 
--
<pre>



解法二：水平扫描  
--
思路：
--
    想象数组的末尾有一个非常短的字符串，使用上述方法依旧会进行 S 次比较。优化这类情况的一种方法就是水平扫描。我们从前往后枚举字符串的每一列，先比较每个字符串相同列上的字符（即不同字符串相同下标的字符）然后再进行对下一列的比较。  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/11 21:59
 * @descriptor  14. 最长公共前缀
 */
public class LongestCommonPrefix_14 {

    public static String longestCommonPrefix(String[] strs) {
        if(strs.length == 0)
            return "";
        String s = strs[0];
        for (int i = 1; i < strs.length; i++) {
            int j = 0;
            for (; j < s.length() && j < strs[i].length(); j++) {
                if(s.charAt(j) != strs[i].charAt(j))
                    break;
            }
            s = s.substring(0,j);
        }
        return s;
    }
    public static void main(String[] args) {
       // String strings[] = {"flowler","flow","flight"};
        String strings[] = {"flowa","flow"};
        String s = longestCommonPrefix(strings);
        System.out.println(s);
    }
}
</pre>
原地址：https://leetcode-cn.com/problems/longest-common-prefix/solution/zui-chang-gong-gong-qian-zhui-by-leetcode/  
