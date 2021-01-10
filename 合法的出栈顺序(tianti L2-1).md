# 合法的出栈顺序(tianti L2-1)

 four's cccc tianti

​      l2-1

## thinking

​	显然，这就是一个显然的数据结构的题，

​	 那么如何解决呢？

### 原有思路



   考虑极端情况，若最后一个元素第一个出栈，则必有比他小的元素全都在栈中则顺序已定。

   当最后一个元素第二个出栈，则必有栈高大于等于size-1、

   然后，然后脑子就炸了。。。



### 递推角度的理解（正确）

 从dp角度理解：

​		当栈高    h==0时，显然只有原顺序合法。

​		当stack h==1时，对于每一个元素的逆序数至多存在一个（之后小于该元素的最多有一条）

​        同理推广到高阶，就有：
​				存在一个stack that high is k ， 

  				对于输出顺序out[n], 对于out[i] 有 逆序数小于等于 k，

​				且所有小于out[i]且在i之后的元素，必须以逆序方式出现。即4在一号位出现则后面1，2，3不管在哪出现必须都是3，2，1这样的顺序

​		   		

​     

~~~ cpp
#include<bits/stdc++.h>
using namespace std;
const int MAXN = 1e5+100;
int a[MAXN];
int nixu(int ind,int siz,int&falg){
    int ans =0;
    int befor=ind;
    for(int i=ind+1;i<siz;i++){
        if(a[i]<a[ind]){
            ans++;
            if(a[befor]<a[i]){//且所有小于out[i]且在i之后的元素，必须以逆序方式出现。
                falg=1;		  //这里直接实现为小于a[i]的元素应当有后一个比前一个大。
                return ans;
            }
            befor = i;
        }
        
    }
    return ans;//对于输出顺序out[n], 对于out[i] 有 逆序数小于等于 k
}
int main()
{
   int n,m,sizeofstack;
   cin>>sizeofstack>>n>>m;;
   for(int we=0;we<m;we++){
       int ans=0;
       for(int s=0;s<n;s++)cin>>a[s];
       for(int i=0;i<n;i++){
           if(nixu(i,n,ans)>=sizeofstack){
                ans=1;
                break;
           }
           if(ans==1)break;
       }
       if(ans==0){
           printf("YES\n");
       }
       else{
           printf("NO\n");                                                      
       }
   
   
   
   }
}
~~~



​	ok，做出来了，直接自己也是大佬了，（可把自己nb坏了，恰会腰.jpg）

### 大佬思路

  

代码如下

   ~~~ cpp
int n;
int a[MAXN];
stack<int>st;
stack<int>res;
cin>>a[n];
st.assign(a.rbegin(),a.rend());
for(int i=1;i<=n;i++){
    res.push(i);
    while(!st.empty() && !res.empty() && res.top()==st.top()){
		st.pop();
        res.pop();
    }
}
if(st.empty())cout<<"YES\n";
else cout<<"NO\n";
   ~~~

