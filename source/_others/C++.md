---
title: C++
date: 2020-06-03 19:02:08
categories: Computer
---

> 针对pat机考的复习整理。有C语言和java的基础，C++边看边学中。

# PAT 甲级 Pactice

## **1001** A+B Format

> **要点**
>
> 1. [string to int and int to string](https://www.systutorials.com/convert-string-to-int-and-reverse/)
> 2. 字串处理（提取substring、erase）[更多string function请参阅](http://www.cplusplus.com/reference/string/basic_string/)

```c++
#include <iostream>
#include <sstream>
#include <string>
using namespace std;
string ToString(unsigned long sum){
    stringstream s;
    s << sum;
    string str = s.str();
    return str;
}
int main(){
    long a, b, sum;
    cin >> a >> b;
    sum = a + b;
    //非正数处理&转字串
    if(sum == 0){
        cout << 0;
        return 0;
    }else if(sum < 0){
        cout << "-";
        sum = -sum;
    }
    string str = ToString(sum);
    //切多出头部
    int n = str.length();
    int x = n % 3;
    cout << str.substr(0, x);
    str.erase(0, x);
    if (n > 3) cout << ",";
    //3个一output
    for(int i = 0; i < n/3 - 1; i++){
        cout << str.substr(0, 3) << ",";
        str.erase(0, 3);
    }
    cout << str;
    return 0;
}
```

## **1002** A+B for Polynomials

> **Tips**
>
> 1. [使用map](https://blog.csdn.net/a845717607/article/details/86508227)存储资料或许是不错的方法，但我习惯了使用struct（大概是冥顽不化叭 ╮(￣▽￣")╭ ）
> 2. [保留位数的表示](https://blog.csdn.net/qq_36667170/article/details/79265224)（C++的表示方法略麻烦，我希望我可以记得住！）
> 3. 注意归零后的细节处理
> 4. 边读入边计算 v.s 统整完所有资料后再计算

```C++
#include <iostream>
#include <cstdlib>
#include <iomanip> //控制输出
using namespace std;
struct POLY{
    int ex;
    double coe;
};
void Print(POLY* p, int n){
    cout.setf(ios::fixed);
    cout<<n;
    for(int i = 0; i < n; i++){ cout <<" "<<p[i].ex <<" "<< setprecision(1)<<p[i].coe; }
    cout<<endl;
}
int main(){
    int N1, N2;
    cin >> N1;
    POLY* p1 = (POLY*) malloc(sizeof(POLY) * N1);
    for(int i = 0; i < N1; i++){ cin >> p1[i].ex >> p1[i].coe; }
    cin >> N2;
    POLY p2, *p = (POLY*) malloc(sizeof(POLY) * (N1+N2));
    int j = 0, k = 0;
    for(int i = 0; i < N2; i++){
        cin >> p2.ex >> p2.coe;
        //sum
        while(p1[j].ex > p2.ex) p[k++] = p1[j++]; //大于
        if(p1[j].ex == p2.ex){ //exponent相同
            p[k] = p2;
            p[k].coe = p1[j++].coe+p2.coe;
            if (p[k].coe != 0) k++;
            continue;
        }
        p[k++] = p2; //小于
    }
    while(j < N1) p[k++] = p1[j++]; //剩余的
    Print(p, k);
    return 0;
}
```

## 1003 Emergency

> **Tips**
>
> 1. [关于vector sort的补充](https://www.itread01.com/content/1544347654.html)  （这个看起来就超级实用的）
> 2. [infinite的表示](https://cloud.tencent.com/developer/ask/96717)
> 3. 审题，我最开始想当然的以为shortest path题要印出的当然是shortest path的长度啦！然后被piapia打脸，debug了N久(*ﾟДﾟ)つﾐ
> 4. Dijkstra Algorithm（lec6）

```c++
/* 1. N M C1 C2: 城市数，道路数，当前位置，目标位置 2. 各城市的救援队数 3. c1 c2 l...
   -> shortest path数量，最大救援数 */
#include <iostream>
#include <vector>
#include <algorithm>
#include <limits>
using namespace std;
int INF = numeric_limits<int>::max();
struct PATH{
    int c;
    int l;
};
vector<int> totR; vector<int> totP;
bool cmp(const PATH &a, const PATH &b) { return a.l > b.l; }
void Dijkstra(vector<PATH> que, vector< vector<int> > l, vector<int> r){
    while(que.size()){
        //sort and get the minimum vertex
        sort(que.begin(), que.end(), cmp);
        vector<PATH>::iterator qit = que.end()-1; que.pop_back();
        int ca = qit->c, la = qit->l;
        //every edge of the vertex
        for(vector<PATH>::iterator it = que.begin(); it != que.end(); it++){
            int cb = it->c, lb = it->l, length = l[ca][cb];
            if(length == INF) continue;
            if(la+length == lb) {
                if(totR[cb] < totR[ca] + r[cb]) totR[cb] = totR[ca] + r[cb];
                totP[cb] += totP[ca];
            }
            if(la+length < lb) { 
                it->l = la+length; 
                totR[cb] = totR[ca] + r[cb]; 
                totP[cb] = totP[ca]; 
            }
        }
    }
}
int main(){
    int N,M,C1,C2; vector<int> rescue;
    cin>>N>>M>>C1>>C2;

    int a, b, c; vector< vector<int> > l(N, vector<int>(N, INF)); 
    for(int i = 0; i < N; i++) { cin>>a; rescue.push_back(a); } 
    while(cin>>a>>b>>c) { l[a][b] = c; l[b][a] = c; } l[C1][C1] = 0;

    totR.resize(N, 0); totP.resize(N, 0);
    totR[C1] = rescue[C1]; totP[C1] = 1;
    PATH p; vector<PATH> pQue;
    for(int i = 0; i < N; i++) { p.c = i, p.l = l[C1][i]; pQue.push_back(p); }
    Dijkstra(pQue, l, rescue);
    cout<<totP[C2]<<" "<<totR[C2]<<endl;
    return 0;
}
```

