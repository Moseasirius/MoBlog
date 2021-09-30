---
title: CSP
date: 2021-04-03 21:08:49
tags: CSP
---

CPS <!--more--> 

202104-1灰度直方图

```C++
#include<iostream>
using namespace std;
int main()
{
    int n,m,l;
	cin>>n>>m>>l;
	int h[256]={0};
	int x;
	for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cin>>x;
			h[x]++;
		}
	}
	for(int i=0;i<l;i++){
		cout<<h[i]<<" ";
	}
	cout<<endl;	
}
```

202104-2邻域均值

```C++
//超时70分，未想出解决超时的办法
#include<iostream>
using namespace std;
#define L 256
#define N 100
int main()
{
	int n,l,r,t;
	cin>>n>>l>>r>>t;
	int h[L]={0};
	int a[N][N]={0};
	int lowt=0;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			cin>>a[i][j];
			h[a[i][j]]++;
		}
	
	}
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
		int maxx=i+r>n-1?n-1:i+r;
		int maxy=j+r>n-1?n-1:j+r;
		int minx=i-r<0?0:i-r;
		int miny=j-r<0?0:j-r;
		double count=0;
		double sum=0;
		for(int x=minx;x<=maxx;x++){
			for(int y=miny;y<=maxy;y++){
				sum+=a[x][y];
				count++;
			}
		}
		sum=sum/count;
		if(sum<=t)lowt++;	
    }
  }
        cout<<lowt;
}
```

### 202012-1期末预测之安全指数

```c++
#include<iostream>
using namespace std;
int main(){
	int n;
	int w,score;
	cin>>n;
	int sum=0;
	for(int i=0;i<n;i++){
		cin>>w>>score;
		sum+=w*score;
	}
	if(sum<0){
		sum=0;
	}
	cout<<sum;
} 
```

### 202012-2期末预测之最佳阈值

```c++
#include<iostream>
#include<algorithm>

using namespace std;
typedef struct Node{
	int theta;
	int predict;
}Node;

bool cmp(Node a,Node b){
	return a.theta<b.theta;
} 
int main(){
	int m;
	Node node[100005];
	int flag0[100005]={0}; //记录小于每个位置点阈值的result=0的个数 
	int flag1[100005]={0}; //记录大于等于每个位置点阈值的result=1的个数  
	cin>>m;
	for(int i=0;i<m;i++){
		cin>>node[i].theta>>node[i].predict;
	}
	sort(node,node+m,cmp); //输入后排序  	
	int thetaid=0;
	int max=0;
//	记录小于每个位置点阈值的result=0的个数
	for(int i=1;i<=m;++i){
		if(node[i].predict==0){
			flag0[i]=flag0[i-1]+1;
		}
		else{
			flag0[i]=flag0[i-1];
		}	
	}
//记录大于等于每个位置点阈值的result=1的个数 	
	for(int i=m;i>=1;--i){
		if(node[i].predict==1){
			flag1[i]=flag1[i+1]+1;}
		else{
			flag1[i]=flag1[i+1];}
	}	

	for(int i=1;i<=m;++i){
		if(node[i].theta==node[i-1].theta){
				continue;}
		if(flag0[i-1]+flag1[i]>=max){
		max=flag0[i-1]+flag1[i];
		thetaid=node[i].theta;}
	}
	cout<<thetaid;
	return 0;
}
```



### 202009-1称检测点查询

```c++
#include<iostream>
#include<math.h>
#include<algorithm> 
using namespace std;

typedef struct Node{
	int x;
	int y;
	int id;
	double distance; 
}Node;

bool cmp (Node a,Node b){
	if(a.distance!=b.distance){
		return a.distance<b.distance;
	}
	return a.id<b.id;
}
//编写sort的排序方法，如果没有，默认从小到大排血 

int main(){
	int n,x,y;
	Node node[500];
	cin>>n>>x>>y;
	for(int i=0;i<n;i++){
		cin>>node[i].x>>node[i].y;
		node[i].id=i+1;
		node[i].distance=sqrt((node[i].x-x)*(node[i].x-x)+(node[i].y-y)*(node[i].y-y));
		
		 
	}
	sort(node,node+n,cmp);
	for(int i=0;i<3;i++){
		cout<<node[i].id<<endl;
	}
} 

```

### 202009-2风险人群筛查

```c++
#include<iostream>
using namespace std;

typedef struct Node{
	int x,y;
	int through,danger,k;
}Node; 
int main(){
	int t,k,n,x1,y1,x2,y2;
	int through=0,danger=0;
	cin>>t>>k>>n>>x1>>y1>>x2>>y2;
	for(int i=0;i<t;i++){
		Node node;
		node.through=0;
		node.danger=0;
		node.k=0;
		for(int j=0;j<n;j++){
			int x,y;
			cin>>x>>y;
			if(x1<=x&&x<=x2&&y1<=y&&y<=y2){
				node.through=1;
				node.k+=1;
				if(node.k==k){
					node.danger=1; 	}
			  }//连续k个或更多坐标均位于矩形内（含边界），
			  //则认为该居民曾在高危区域逗留。 
			else node.k=0 ;  
			} 	
			through+=node.through;
			danger+=node.danger;
	}		
	cout<<through<<endl<<danger;
}
```

### 202006-1线性分类器

```C++
#include<iostream>
#include<set>
#include<algorithm> 
using namespace std; 

typedef struct Node{
	double x,y;
	char type;
}Node;

int main(){
	int n,m;
	Node node[1001];
	cin>>n>>m;
	for (int i=0;i<n;i++){
		cin>>node[i].x>>node[i].y>>node[i].type;		
	}
	
	double n0,n1,n2;
	
	while(m--){
		cin>>n0>>n1>>n2;
		set<char> up,down;
		for( int i=0;i<n;i++){
			if(n0+n1*node[i].x+n2*node[i].y>0){
				up.insert(node[i].type);
			}else {
		     	down.insert(node[i].type);
		    }
		}
	//在set中，size()返回的元素种类的个数，同一种元素即使有很多个，也算一个
	//所以我们可以用来判断分类是否正确，
	//如果set不是同一种元素，即size()的值大于1，则分类错误，反之则正确 
	if(up.size()>1||down.size()>1){
		cout<<"No"<<endl;
	}
	else {
	cout<<"Yes"<<endl;
    }
	}	
}
```

### 202006-2稀疏向量解法一

```C++
#include<iostream>
using namespace std;
int main(){
	int n,a,b;
	cin>>n>>a>>b;
	int index,value;
	long long result=0;

	int *arraya=new int[n];
	int *arrayb=new int[n];
	
	for(int i=0;i<n;i++){
		arraya[i]=0;
		arrayb[i]=0;
	}
	for(int i=0;i<a;i++){
		cin>>index>>value;
		arraya[index]=value;
	}
	for(int j=0;j<b;j++){
		cin>>index>>value;
		arrayb[index]=value;
	}
	for(int k=0;k<n;k++){
		result+=arraya[k]*arrayb[k];	
	}
	cout<<result<<endl;	
	delete [] arraya; 
	delete [] arrayb; 
	return 0;
} 
```

