## 迷宫

### Code

```cpp
#include<bits/stdc++.h>
using namespace std;
int const dx[4]={-1,0,1,0},dy[4]={0,-1,0,1};//往 左/上/右/下 走时x坐标和y坐标的变化
int m[11][11],n;//地形（1和0表示） 以及 地图边长
bool used[11][11];//走过之处就不用再走第二遍了6
int dfs(int x,int y,int tim){//现在那个人走到的坐标
	if(tim>n*n)return 0;//全图都走一遍还没走到就是不能到终点了（不用也行）
	if(x==n&&y==n)return 1;/到了目的地，方案数就加一
	int ans=0;//方案数
	for(int i=1;i<=4;i++){//上下左右
		int a=x+dx[i],b=y+dy[i];//往对应方向走后坐标
		if(a>=1&&a<=n&&b>=1&&b<=n&&m[a][b]!=1&&!used[a][b])//没有越界，不是障碍物，没走过
      used[a][b]=true,ans+=dfs(a,b,tim+1);//标记走过了，方案数加上从下个位置去终点的方案数
	}
	return ans;
}
int main(){
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
		for(int j=1;j<=n;j++)
			scanf("%d",&m[i][j]);
	used[1][1]=true;//出发地肯定走过了
	if(dfs(1,1,0)==0)printf("NO");//原来是要求能不能走到啊，白忙活了
	else printf("YES");
	return 0;
}
```
***
