# KMP 字符串匹配算法学习

把返回第一次匹配的之后，继续匹配后面的字符。
用数组来保存出现的位置，每当匹配到时i设为匹配下标，j置0

# 改之前的
```java
  public static int kmp(String str, String dest,int[] next){//str文本串  dest 模式串
    	//List al=new ArrayList<>();
        for(int i = 0, j = 0; i < str.length(); i++){
            while(j > 0 && str.charAt(i) != dest.charAt(j)){
                j = next[j - 1];
            }
            if(str.charAt(i) == dest.charAt(j)){
                j++;
            }
            if(j == dest.length()){
                return i-j+1;
            	//i=i-j+1;
            	//al.add(i);
            	//j=0;
            	
            }
            
        }
        return 0;
        //return al;
    }
```

# 这个改之后的
```java
public class KMP {
    public static List kmp(String str, String dest,int[] next){//str文本串  dest 模式串
    	List al=new ArrayList<>();
        for(int i = 0, j = 0; i < str.length(); i++){
            while(j > 0 && str.charAt(i) != dest.charAt(j)){
                j = next[j - 1];
            }
            if(str.charAt(i) == dest.charAt(j)){
                j++;
            }
            if(j == dest.length()){
                //return i-j+1;
            	i=i-j+1;            //i置返回下标
            	al.add(i);          //匹配到下标放入数组
          	j=0;                  //j重置0
            	
            }
            
        }
        //return 0;
        return al;
    }
    public static int[] kmpnext(String dest){
        int[] next = new int[dest.length()];
        next[0] = 0;
        for(int i = 1,j = 0; i < dest.length(); i++){
            while(j > 0 && dest.charAt(j) != dest.charAt(i)){
                j = next[j - 1];
            }
            if(dest.charAt(i) == dest.charAt(j)){
                j++;
            }
            next[i] = j;
        }
        return next;
    }
    public static void main(String[] args){
        String a = "aba";
        String b = "ssdfgasdbababa";
        int[] next = kmpnext(a);
        List res = kmp(b, a,next);
        System.out.println(res);
        //for(int i = 0; i < next.length; i++){
           // System.out.println(next[i]);            
        //}
       // System.out.println(next.length);
    }
}
```






