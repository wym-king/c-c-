# c-c-
some codes for competiion
#include<algorithm>
#include <iostream>
#include <stdlib.h>
#include <string.h>
#include  <stdio.h>
#include   <math.h>
#include   <time.h>
#include   <vector>
#include   <bitset>
#include    <queue>
#include      <map>
#include      <set>
using namespace std;
 
char s[16][16],w[16][16];
int Ans;
 
void Rot(int a,int b)
{
    for(int i=0;i<4;i++)
        for(int j=0;j<4;j++)
            w[j][3-i]=s[a+i][b+j];
    for(int i=0;i<4;i++)
        for(int j=0;j<4;j++)
            s[a+i][b+j]=w[i][j];
}
 
int tot,vis[16];
 
bool check(int a,int b)
{
    for(int i=a;i<a+4;i++)
    {
        tot++;
        for(int j=0;j<b+4;j++)
        {
            if(vis[s[i][j]]==tot)
                return 0;
            vis[s[i][j]]=tot;
        }
    }
    for(int i=b;i<b+4;i++)
    {
        tot++;
        for(int j=0;j<a+4;j++)
        {
            if(vis[s[j][i]]==tot)
                return 0;
            vis[s[j][i]]=tot;
        }
    }
    return 1;
}
 
void dfs(int i,int j,int k)
{
    if(i==4)
    {
        Ans=min(Ans,k);return;
    }
    if(k>=Ans)
        return;
    if(j==4)
        return dfs(i+1,0,k);
    for(int t=0;t<4;t++)
    {
        if(check(i*4,j*4))
            dfs(i,j+1,k+t);
        Rot(i*4,j*4);
    }
}
 
void solve()
{
    for(int i=0;i<16;i++)
        scanf(" %s",s[i]);
    for(int i=0;i<16;i++)
        for(int j=0;j<16;j++)
            if(s[i][j]<='9')
                s[i][j]-='0';
            else
                s[i][j]=s[i][j]-'A'+10;
    Ans=1000;dfs(0,0,0);
    cout<<Ans<<endl;
}
 
int main()
{
    int t;cin>>t;
    while(t--)
        solve();
    return 0;
}
