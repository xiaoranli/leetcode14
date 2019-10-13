3、leetcode14. 最长公共前缀
==
解法一：  
--
思路：
--
    当字符串数组长度为 0 时则公共前缀为空，直接返回,令最长公共前缀 ans 的值为第一个字符串，进行初始化,遍历后面的字符串，依次将其与 ans 进行比较，两两找出公共前缀，最终结果即为最长公共前缀,如果查找过程中出现了 ans 为空的情况，则公共前缀不存在直接返回。  
时间复杂度：O(s)，s 为所有字符串的长度之和  
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
