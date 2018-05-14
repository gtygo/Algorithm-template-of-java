# 		

# 		Algorithm template of java

​																			by : gaotianyi





















































##### 输入挂

```java
	static class InputReader{
		BufferedReader buf;
		StringTokenizer tok;
		InputReader(){
			buf=new BufferedReader(new InputStreamReader(System.in));
		}
		boolean hasNext(){
			while(tok==null||!tok.hasMoreElements()){
				try{
					tok=new StringTokenizer(buf.readLine());
				}catch (Exception e){
					return false;
				}
			}
			return true;
		}
		String next(){
			if(hasNext()){
				return tok.nextToken();
			}return null;
		}
		int nextInt(){
			return Integer.parseInt(next());
		}
		double nextDouble(){
			return Double.parseDouble(next());
		}
		long nextLong(){
			return Long.parseLong(next());
		}
		BigInteger nextBigInteger(){
			return new BigInteger(next());
		}
		BigDecimal nextBigDecimal(){
			return new BigDecimal(next());
		}
	}
```

##### 扩展欧几里得

```java
	static long x,y;
	static long extgcd(long a,long b){
		if(b==0){
			x=1; y=0; return a;
		}
		long d=extgcd(b,a%b);
		long t=x; x=y;y=t-a/b*x;
		return d;
	}
```

##### 快速幂

```java
	static long powmod(long a,long n,long c){
		long ans=1;
		while(n!=0){
			if( (n&1)!=0 ){
				ans*=a;
				ans%=c;
			}
			a*=a;
			a%=c;
			n>>=1;
		}
		return ans;
	}
```

##### 中国剩余定理

```java
public static void main(String []args){
		InputReader in=new InputReader();
		int n=in.nextInt();
		int a[]=new int[n+2];
		int b[]=new int[n+2];
		for(int i=0;i<n;i++){
			a[i]=in.nextInt();
			b[i]=in.nextInt();
		}
		int k=1;int sum=b[0];
		for(int i=0;i<n-1;i++){
			k*=a[i];
			while(sum%(a[i+1])!=b[i+1]){
				sum+=k;
			}
		}
		System.out.println(sum);

	}
```

##### 求1/n循环节

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.nio.Buffer;
import java.util.*;
//如果1<=b<a,a没有2或5的质因子，并且a与b互质，那么b/a 的循环节位数恰好等于min(10e≡1(moda)),e是正整数。
//如果1<=b<a,a没有2或5的质因子，并且a与b互质，那么b/a 的循环节位数必整除ϕ(a)

public class Main {
	public static void main(String []args) {
		Scanner in=new Scanner(System.in) ;
		int maxn=1005;
		int res[]=new int[maxn];
		int i,j,n;
		for(int temp=1;temp<=1000;temp++){
			i=temp;
			while(i%2==0){
				i/=2;
			}
			while(i%5==0){
				i/=5;
			}
			n=1;
			for(j=1;j<=i;j++){
				n*=10; n%=i;
				if(n==1) {
					res[temp] = j;
					break;
				}
			}
		}
		int max_re;
		n=in.nextInt();
		max_re=1;
		for(i=1;i<=n;i++){
			if(res[i]>res[max_re]){
				max_re=i;
			}
		}
		System.out.println(max_re);
	}
}

```

##### 素数筛

```java
	static boolean is_prime[]=new boolean[N];
	static int prime[]=new int[N];	
	static int prime1(int n){  //常规筛法
		//2 3 5 7为素数 1 不是素数
		int p=0;
		for(int i=0;i<=n;i++){
			is_prime[i]=true;
		}
		is_prime[0]=is_prime[1]=false;
		for(int i=2;i<=n;i++){
			if(is_prime[i]){
				prime[p++]=i;
				for(int j=2*i;j<=n;j+=i){
					is_prime[j]=false;
				}
			}
		}
		return p;
	}
	
	static int prime2(int n){   //线性素数筛
		int num=0,i,j;
		for(i=2;i<n;i++){
			if(!is_prime[i]) prime[num++]=i;
			for(j=0;(j<num && i*prime[j]<n);j++){
				is_prime[i*prime[j]]=true;
				if((i%prime[j])==0)
					break;
			}
		}
		return num;
	}
```



##### 树状数组

```java
static int lowbit(int x)  
{  
    return x & (-x);      
}   
static int getSum(int x)  
{  
    int s = 0;  
    for(int i = x; i; i -= lowbit(i))  
        s += c[i];  
    return s;  
}     
static void add(int x, int val)  
{  
    for(int i = x; i < MAXN; i += lowbit(i)){  
        c[i] += val;  
    }  
}  
```

##### 邻接表

```java
		int u[]=new int[inf];
		int v[]=new int[inf];
		int w[]=new int[inf];
		int first[]=new int[200];
		int next[]=new int[200];
		int n=in.nextInt(); int m=in.nextInt();
		for(int i=1;i<=n;i++){
			first[i]=-1;
		}
		for(int i=1;i<=m;i++){
			u[i]=in.nextInt(); v[i]=in.nextInt(); w[i]=in.nextInt();
			//构建邻接表
			next[i]=first[u[i]];
			first[u[i]]=i;
		}
		//遍历邻接表
		int k=first[1];
		for(int i=1;i<=n;i++) {
			k=first[i];
			while (k != -1) {
				System.out.println(u[k] + " " + v[k] + " " + w[k]);
				k = next[k];
			}
		}
```

##### 邻接表深搜

```java
static void dfs(int cur){
		if(cur==n) return ;
		int k;
		k=first[cur];
		
		while(k!=-1){
			System.out.println(u[k]+" "+v[k]);
			dfs(v[k]);
			k=next[k];
		}
	}
```

#####并查集

```java
	static int par[];
	static void  init(int n){
		par=new int[n+2];
		for(int i=1;i<=n;i++) par[i]=i;
	}
	static int find(int x){
		if(par[x]==x)return x;
		else return par[x]=find(par[x]);
	}
	static  boolean union(int x,int y){
		int tx=find(x); int ty=find(y);
		if(tx==ty) return false;
		par[tx]=ty; return true;
	}
	static boolean same(int x,int y){
		return find(x)==find(y);
	}
```

##### Kruskal

```java
	static int V,E; //点 边
	static class edge implements Comparable<edge>{
		int u;int v; int cost;
		edge(int x,int y,int z){
			u=x;v=y;cost=z;
		}
		@Override
		public int compareTo(edge o) {
			return this.cost>o.cost?1:-1;
		}
	}
	static List<edge> es=new ArrayList<edge>();
	static int Kruskal(){
		Collections.sort(es);
		init(E);
		int res=0;  //最小生成树权变之和
		for(int i=0;i<E;i++){
			if(union(es.get(i).u,es.get(i).v)){
				res+=es.get(i).cost;
			}
		}
		return res;
	}
```

##### Prim

```java
	static int V,E;
	final static int inf=10001;
	static int cost[][];
	static int mincost[]; 	//从集合x出发到每个点的最短距离
	static boolean used[];	//定点i是否在集合x中
	static int prim(){ 		//由普通的邻接矩阵构成的数据结构 时间复杂度为 O(N^2)
		for(int i=1;i<=V;i++){ 	//范围依照点的取值而确定
			
			mincost[i]=inf;
			used[i]=false;
		}
		mincost[1]=0;  //如果点的编号从零开始则将mincost[0]赋值为零
		int res=0;
		while(true){
			int v=-1;
			for(int u=1;u<=V;u++){
				if(!used[u]&&(v==-1||mincost[u]<mincost[v]))
					v=u;
			}
			if(v==-1)
				break;
			used[v]=true;
			res+=mincost[v];
			
			for(int u=1;u<=V;u++){
				mincost[u]=Math.min(mincost[u],cost[v][u]);
			}
		}
		return res;
	}
```

##### Dijkstra

```java
public class dijkstra {
	static int map[][]=new int[10][10];
	static int dis[]=new int[10];
	static int mark[]=new int[10];
	static int i,j,n,m,t1,t2,t3,u,v,min;
	static int inf=9999999;
	public static void main(String []args){
		Scanner in=new Scanner(System.in);
		n=in.nextInt(); m=in.nextInt();
		for(i=1;i<=n;i++){
			for(int j=1;j<=n;j++){
				if(i==j)
					map[i][j]=0;
				else{
					map[i][j]=inf;
				}
			}
		}
	for(i=1;i<=m;i++){
			t1=in.nextInt(); t2=in.nextInt(); t3=in.nextInt();
			map[t1][t2]=t3;
	}
	for(i=1;i<=n;i++) dis[i]=map[1][i];
	
	for(i=1;i<=n;i++)
		mark[i]=0;
	mark[1]=1;
	for(i=1;i<=n-1;i++){
		min=inf;
		for(j=1;j<=n;j++){
			if(mark[j]==0&&dis[j]<min){
				min=dis[j];
				u=j;
			}
		}
		mark[u]=1;
		for(v=1;v<=n;v++){
			if(map[u][v]<inf){
				if(dis[v]>dis[u]+map[u][v])
					dis[v]=dis[u]+map[u][v];
			}
		}
	}
	for(i=1;i<=n;i++)
		System.out.println(dis[i]);
	}
}
```

##### Spfa 数组版

```java
	public static void main(String []args){
		Scanner in=new Scanner(new BufferedInputStream(System.in));
		int n,m,i,j,k;
		int u[]=new int[8];
		int v[]=new int[8];
		int w[]=new int[8];
		int first[]=new int[6];
		int next[]=new int[8];
		int dis[]=new int[6];
		int mark[]=new int[6];
		int que[]=new int[101]; int head=1;int tail=1;
		int inf=99999999;
		n=in.nextInt(); m=in.nextInt();
		for(i=1;i<=n;i++)
			dis[i]=inf;
		dis[1]=0;// 从几号定点开始
		for(i=1;i<=n;i++) mark[i]=0;
		for(i=1;i<=n;i++) first[i]=-1;
		for(i=1;i<=m;i++){
			u[i]=in.nextInt();
			v[i]=in.nextInt();
			w[i]=in.nextInt();
			
			next[i]=first[u[i]];
			first[u[i]]=i;
		}
		que[tail]=1;tail++;
		
		while(head<tail){
			k=first[que[head]];
			while(k!=-1){
				if(dis[v[k]]>dis[u[k]]+w[k]){
					dis[v[k]]=dis[u[k]]+w[k];
					if(mark[v[k]]==0){
						que[tail]=v[k];
						tail++;
						mark[v[k]]=1;
					} }
				k=next[k];
			}
			mark[que[head]]=0;
			head++;
		}
		for(i=1;i<=n;i++)
			System.out.println(dis[i]);
}
```

##### SPFA 类版

```java

public class Main {
	static public long []result;
	static class edge{
		public int a;
		public int b;
		public int value;
		edge(int a,int b,int value){
			this.a=a;
			this.b=b;
			this.value=value;
		}
	}
	static public boolean getShortestPaths(int n,int s,edge[] A){
		ArrayList<Integer> list=new ArrayList<Integer>();
		result=new long[n];
		boolean []used=new boolean[n];
		int []num=new int[n];
		for(int i=0;i<n;i++){
			result[i]=Integer.MAX_VALUE;
			used[i]=false;
		}
		result[s]=0;
		used[s]=true;
		num[s]=1;
		list.add(s);
		while(list.size()!=0){
			int a=list.get(0);
			list.remove(0);
			for(int i=0;i<A.length;i++){
				if(a==A[i].a&&result[A[i].b]>result[A[i].a]+A[i].value){
					result[A[i].b]=result[A[i].a]+A[i].value;
					if(!used[A[i].b]){
						list.add(A[i].b);
						num[A[i].b]++;
						if(num[A[i].b]>n)
							return false;
						used[A[i].b]=true;
					}
				}
			}
			used[a]=false;
		}
		return true;
	}
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int n=in.nextInt(); int s=in.nextInt(); int p=in.nextInt();
		edge[] A=new edge[p];
		for(int i=0;i<p;i++){
			int a=in.nextInt();
			int b=in.nextInt();
			int value=in.nextInt();
			A[i]=new edge(a,b,value);
		}
		if(getShortestPaths(n,s,A)){
			for(int i=0;i<result.length;i++){
				System.out.println(result[i]+" ");
			}
		}else{
			System.out.println("error");
		}
	}
}
```

##### 割点

```java

public class Main {
	static int n,m,e[][]=new int[9][9],root;
	static int num[]=new int[9],low[]=new int[9],flag[]=new int[9],index=0;
	static void dfs(int cur,int father){
		int child=0;
		index++;
		num[cur]=index;
		low[cur]=index;
		for(int i=1;i<=n;i++){
			if(e[cur][i]==1){
				if(num[i]==0){
					child++;
					dfs(i,cur);
					low[cur]=Math.min(low[cur],low[i]);
					if(cur!=root && low[i]>=num[cur]){
						flag[cur]=1;
					}
					if(cur==root && child==2){
						flag[cur]=1;
					}
				}else if(i!=father){
					low[cur]=Math.min(low[cur],num[i]);
				}
			}
		}
	}
	public static void main(String []args){
		Scanner in=new Scanner(System.in);
		 n=in.nextInt();  m=in.nextInt();
		for(int i=1;i<=m;i++){
			int x=in.nextInt(); int y=in.nextInt();
			e[x][y]=1; e[y][x]=1;
		}
		root=1;
		dfs(1,root);
		for(int i=1;i<=n;i++){
			if(flag[i]==1){
				System.out.println(i);
			}
		}	
	}
}

```

##### 割边

```java
public class Main {
	static int n,m,e[][]=new int[9][9],root;
	static int num[]=new int[9],low[]=new int[9],index;
	static void dfs(int cur,int father){
		int i,j;
		index++;
		num[cur]=index;
		low[cur]=index;
		for(i=1;i<=n;i++){
			if(e[cur][i]==1){
				if(num[i]==0){
					dfs(i,cur);
					low[cur]=Math.min(low[i],low[cur]);
					if(low[i]>num[cur]){
						System.out.println(cur+"-"+i);
					}
				}else if(i!=father){
					low[cur]=Math.min(low[cur],num[i]);
				}
			}
		}
	}
	public static void main(String []args){
		Scanner in=new Scanner(System.in);
		n=in.nextInt(); m=in.nextInt();
		for(int i=1;i<=m;i++){
			int x=in.nextInt(); int y=in.nextInt();
			e[x][y]=1;
			e[y][x]=1;
		}
		root=1;
		dfs(1,root);
	}
}

```

##### 二分图最大匹配(匈牙利算法)

```java
public class Main {
	static int e[][]=new int[101][101];
	static int match[]=new int[101]; //记录配对关系
	static int book[]=new int[101];
	static int n,m;
	static int dfs(int u){
		int i;
		for(i=1;i<=n;i++){
			if(book[i]==0&&e[u][i]==1){
				book[i]=1;
				if(match[i]==0||dfs(match[i])!=0){
					match[i]=u;
					match[u]=i;
					return 1;
				}
			}
		}
		return 0;
	}
	public static void main(String []args){
		Scanner in=new Scanner(System.in);
		int t1,t2,sum=0;
		n=in.nextInt(); m=in.nextInt();
		for(int i=1;i<=m;i++){
			t1=in.nextInt(); t2=in.nextInt();
			e[t1][t2]=1;
			e[t2][t1]=1;
		}
		for(int i=1;i<=n;i++){
			for(int j=1;j<=n;j++){
				book[j]=0;
			}
			if(dfs(i)!=0){
				sum++;
			}
		}
		System.out.println(sum);
	}
}
```

