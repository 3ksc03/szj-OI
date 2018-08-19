## 传送带

## 主要思路：模拟退火（可以上网查一下，很神奇的）
## 类似贪心，但有一些概率“不贪”，避免卡在极优情况（局部最优）
## 就是随便在某条边上找个点，和方向，往那边走
## 若情况更好，采用，else有一定几率采用
## 其实有一定蒙的嫌疑（不过AC就行了）

### Code

```cpp
#include<bits/stdc++.h>
#pragma GCC optimize(2)
#pragma GCC optimize("O3")//手动吸氧
using namespace std;
const double R=0.98;//模拟退火中每次损耗的能量为2%(其实别的也行，只要不太离谱)
double ax,ay,bx,by,cx,cy,dx,dy,p,q,r,ans;
double f(double a,double b,double c,double d){
	return sqrt((a-c)*(a-c)+(b-d)*(b-d));//求两点距离
}
int main(){
    srand(time(0));
    scanf("%lf%lf%lf%lf",&ax,&ay,&bx,&by);
    scanf("%lf%lf%lf%lf%lf%lf%lf",&cx,&cy,&dx,&dy,&p,&q,&r);
    double ab=f(ax,ay,bx,by),cd=f(cx,cy,dx,dy),ac=f(ax,ay,cx,cy);
    double bc=f(bx,by,cx,cy),ad=f(ax,ay,dx,dy),bd=f(bx,by,dx,dy);
    ans=min(min(ad/r,ab/p+bd/r),min(ab/p+bc/r+cd/q,ac/r+cd/q));//answer初始化为min（A->D,A->B->D,A->C->D,A->B->C->D）
    for(int i=1;i<=100;i++){//强行退火100次
    	double tx=ax,ty=ay,px=bx,py=by,mx,my,T=12345678;//T表示初始热量（概率）
	    while(sqrt((tx-px)*(tx-px)+(ty-py)*(ty-py))>0.01){//浩大的枚举工程（A->D,A->B->D,A->C->D,A->B->C->D）中找点
    	    mx=(tx+px)/2,my=(ty+py)/2;
        	double fu=f(mx,my,ax,ay)/p+f(mx,my,dx,dy)/r;
    	    if(fu<ans){
        	    ans=fu;
            	if(rand()%2)tx=mx,ty=my;
	            else px=mx,py=my;
    	    }
        	else
            	if(rand()<T){
                	if(rand()%2)tx=mx,ty=my;
                	else px=mx,py=my;
                	T*=R;
            	}
    	}
    	tx=cx,ty=cy,px=dx,py=dy,T=12345678;
    	while(f(tx,ty,px,py)>0.01){
        	mx=(tx+px)/2,my=(ty+py)/2;
	        double fu=f(mx,my,ax,ay)/r+f(mx,my,dx,dy)/q;
    	    if(fu<ans){
        	    ans=fu;
            	if(rand()%2)tx=mx,ty=my;
    	        else px=mx,py=my;
        	}
    	    else
        	    if(rand()<T){
            	    if(rand()%2)tx=mx,ty=my;
                	else px=mx,py=my;
        	        T*=R;
            	}
    	}
    	tx=ax,ty=ay,px=bx,py=by,mx,my,T=12345678;
    	while(sqrt((tx-px)*(tx-px)+(ty-py)*(ty-py))>0.01){
        	mx=(tx+px)/2,my=(ty+py)/2;
        	double fu=f(mx,my,ax,ay)/p+f(mx,my,cx,cy)/r+cd/q;
    	    if(fu<ans){
        	    ans=fu;
            	if(rand()%2)tx=mx,ty=my;
        	    else px=mx,py=my;
    	    }
        	else
            	if(rand()<T){
            	    if(rand()%2)tx=mx,ty=my;
        	        else px=mx,py=my;
    	            T*=R;
	            }
    	}
    	tx=cx,ty=cy,px=dx,py=dy,T=12345678;
    	while(f(tx,ty,px,py)>0.01){
	        mx=(tx+px)/2,my=(ty+py)/2;
        	double fu=f(mx,my,bx,by)/r+f(mx,my,dx,dy)/q+ab/p;
    	    if(fu<ans){
        	    ans=fu;
            	if(rand()%2)tx=mx,ty=my;
            	else px=mx,py=my;
        	}
        	else
            	if(rand()<T){
        	        if(rand()%2)tx=mx,ty=my;
    	            else px=mx,py=my;
	                	T*=R;
            	}
    	}
    }
    printf("%.2f",ans);//更新无数次后完美的答案 嘿嘿
    return 0;
}
```
***
