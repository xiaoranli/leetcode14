3、leetcode14. 最长公共前缀
==
解法一：水平扫描  
--
思路：
--
    先找前两个字符串公共前缀pre,在找公共前缀pre和第三个字符串的公共前缀pre1,依次类推，当preX=""时停止，否知直到找到最后一个字符串。  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/11 21:59
 * @descriptor  14. 最长公共前缀
 */
public class LongestCommonPrefix_14 {
 public static String longestCommonPrefix2(String[] strs) {
        if (strs.length == 0) return "";
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) return "";
            }
        }
        return prefix;
    }
      public static void main(String[] args) {
       // String strings[] = {"flowler","flow","flight"};
        String strings[] = {"flowa","flow"};
        String s = longestCommonPrefix(strings);
        System.out.println(s);
    }
}
</pre>

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
解法三：分治  
--
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/11 21:59
 * @descriptor  14. 最长公共前缀
 */
 public class LongestCommonPrefix_14 {
  public static String longestCommonPrefix5(String[]strs){
        if(strs == null || strs.length == 0)
            return "";
       return longestCommonPrefix(strs,0,strs.length-1);
    }

    public static String longestCommonPrefix(String[]strs,int l,int r){
        if(l == r)
            return strs[l];
        else{
            int mid  = (l + r) / 2;
            String left = longestCommonPrefix(strs,l,mid);
            String right = longestCommonPrefix(strs,mid+1,r);
            return commonPrefix(left,right);
        }
    }

    public static String commonPrefix(String left,String right){
        int len = Math.min(left.length(),right.length());
        for (int i = 0; i < len; i++) {
            if(left.charAt(i) != right.charAt(i))
                return left.substring(0,i);
        }
        return left.substring(0,len);
    }
     public static void main(String[] args) {
       // String strings[] = {"flowler","flow","flight"};
        String strings[] = {"flowa","flow"};
        String s = longestCommonPrefix(strings);
        System.out.println(s);
    }
}
</pre>
 解法四：KMP  
--  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/13 8:44
 * @descriptor  28. 实现 strStr()
 */
public class StrStr_28 {
    public static int strStr(String haystack,String needle){
        if (needle.equals("")) {
            return 0;
        }
        char[] hChars = haystack.toCharArray();
        char[] nChars = needle.toCharArray();
        int i = 0;
        int j = 0;
        int[] next = getNext(nChars);
        while(i < hChars.length && j < nChars.length){
            if(hChars[i] == nChars[j]){
                i++;
                j++;
            }else if(next[j] == -1)
                i++;
            else{
                j = next[j];
            }
        }
        return j == nChars.length ? i - j : -1;
    }

    private static int[] getNext(char[] str2) {
        if (str2.length == 1) {
            return new int[] { -1 };
        }
        int[] next = new int[str2.length];
        next[0] = -1;//默认
        next[1] = 0;//默认
        int i = 2;//要求的最大相同前后缀 的 每一个位置,第i个位置
        int cn = 0;//跳到的位置,前缀的下一个字符
        while (i < next.length) {
            //i前一个字符与跳到的字符相同，长度为++cn的值
            if (str2[i - 1] == str2[cn]) {
                next[i++] = ++cn;
                //i前一个字符与跳到的字符不等，cn继续向前跳到next[cn]
            } else if (cn > 0) {
                cn = next[cn];
            } else {
                next[i++] = 0;
            }
        }
        return next;
    }

    public static void main(String[] args) {
        //int i = strStr("hello", "ll");
        //int i = strStr("hello", "ll");
        int i = strStr("", "a");
        System.out.println(i);
    }
}
</pre>
原地址：https://leetcode-cn.com/problems/longest-common-prefix/solution/zui-chang-gong-gong-qian-zhui-by-leetcode/  
