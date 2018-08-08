## n皇后问题

### Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int n,qy[11];
bool used[11][11],flag=false;
void setused(int x,int y){//放置皇后之后标注更多不可放置之处
	for(int i=1;i<=n;i++)
		used[x][i]=used[i][y]=true;
	int i=x,j=y;
	while(++i<=n&&++j<=n&&i>=1&&j>=1)
		used[i][j]=true;
	i=x,j=y;
	while(--i<=n&&--j<=n&&i>=1&&j>=1)
		used[i][j]=true;
	i=x,j=y;
	while(--i<=n&&++j<=n&&i>=1&&j>=1)
		used[i][j]=true;
	i=x,j=y;
	while(++i<=n&&--j<=n&&i>=1&&j>=1)
		used[i][j]=true;
	return;
}
void reset(int x,int y){//dfs中撤销setused的标记
	for(int i=1;i<=n;i++)
		used[x][i]=used[i][y]=false;
	int i=x,j=y;
	while(++i<=n&&++j<=n&&i>=1&&j>=1)
		used[i][j]=false;
	i=x,j=y;
	while(--i<=n&&--j<=n&&i>=1&&j>=1)
		used[i][j]=false;
	i=x,j=y;
	while(--i<=n&&++j<=n&&i>=1&&j>=1)
		used[i][j]=false;
	i=x,j=y;
	while(++i<=n&&--j<=n&&i>=1&&j>=1)
		used[i][j]=false;
	return;
}
void dfs(int y){//y表示到了第几行
	if(y==n+1){
		flag=true;//表示有答案
		for(int i=1;i<=n;i++)
			printf("%d ",qy[i]);
		printf("\n");
		return;
	}
	for(int i=1;i<=n;i++)//枚举哪列可以放
		if(!used[i][y]){
			qy[y]=i;
			setused(i,y);
			dfs(y+1);
			reset(i,y);
			for(int i=1;i<y;i++)
				setused(qy[i],i);//防止reset后本来有的前几个皇后的攻击范围被撤销，重新set一遍
		}
	return;
}
int main(){
	scanf("%d",&n);
	dfs(1);
	if(!flag)printf("no solution!");
	return 0;
}
```
***
