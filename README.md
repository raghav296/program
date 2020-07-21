#include<stdio.h>
#include<sys/time.h>
#include<time.h>
#include<sys/resource.h>
void main()
{
int n,i,j,a[10][10],s[10],d[10],v,k,min,u;
struct timeval tv1,tv2;
struct rusage r_usage;
printf("enter the number of vertices\n");
scanf("%d",&n);
printf("enter the cost matrix \n");
printf("enter 999 if no edge between vertices \n");
for(i=1;i<=n;i++)
for(j=1;j<=n;j++)
scanf("%d",&a[i][j]);
printf("enter the source vertex \n");
scanf("%d",&v);
for(i=1;i<=n;i++)
{
s[i]=0;
d[i]=a[v][i];
}
gettimeofday(&tv1,NULL);
d[v]=0;
s[v]=1;
for(k=2;k<=n;k++)
{
min=999;
for(i=1;i<=n;i++)
if(s[i]==0&&d[i]<min)
{
min=d[i];
u=i;
}
s[u]=1;
for(i=1;i<=n;i++)
if(s[i]==0)
{
if(d[i]>(d[u]+a[u][i]))
d[i]=d[u]+a[u][i];
}
}
gettimeofday(&tv2,NULL);
printf("the shortest distance from %d is \n",v);
for(i=1;i<=n;i++)
printf("%d-->%d=%d\n",v,i,d[i]);
printf("time of djikstra=%f microseconds \n",(double)(tv2.tv_usec-tv1.tv_usec));
getrusage(RUSAGE_SELF,&r_usage);
printf("memory usage=%ld kilobytes \n",r_usage.ru_maxrss);
}
