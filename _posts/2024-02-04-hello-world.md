---
layout: post
title:  "leetcode biweekly contest 123"
date:   2024-02-04 13:17:11 +0100
categories: jekyll update
---
"3024. Type of Triangle II"

{% highlight ruby %}
class Solution {
public:
    string triangleType(vector<int>& a) {
        sort(begin(a),end(a));
        if(a[0]+a[1]<=a[2]) return "none";
        if(a[0]==a[1] && a[0]==a[2]) return "equilateral";
        if(a[0]==a[1]||a[1]==a[2]) return "isosceles";
        if(a[0]!=a[1] && a[1]!=a[2]) return "scalene";
        return "";
    }
};
{% endhighlight %}

"3025. Find the Number of Ways to Place People I"
{% highlight ruby %}
class Solution {
public:
    bool ok(vector<vector<int>>&a,int i,int j) {
        if(a[i][0]==a[j][0]) {
            for(int k=0;k<a.size();k++) {
                if(k==i||k==j) continue;
                if(a[k][0]==a[i][0] && a[k][1]>=min(a[i][1],a[j][1]) && a[k][1]<=max(a[i][1],a[j][1])) return false;
            }
        }
        if(a[i][1]==a[j][1]) {
            for(int k=0;k<a.size();k++) {
                if(k==i||k==j) continue;
                if(a[k][1]==a[i][1] && a[k][0]>=min(a[i][0],a[j][0]) && a[k][0]<=max(a[i][0],a[j][0])) return false;
            }            
        }
        for(int k=0;k<a.size();k++) {
            if(k==i||k==j) continue;
            if(a[k][0]>=a[i][0] && a[k][0]<=a[j][0] && a[k][1]>=a[j][1] && a[k][1]<=a[i][1]) return false;
        }
        return true;
    }
    int numberOfPairs(vector<vector<int>>& a) {
        int res=0;
        int n=a.size();
        sort(begin(a),end(a));
        for(int i=0;i<n;i++) {
            for(int j=i+1;j<n;j++) {
                if(a[i][0]!=a[j][0] && a[j][1]>a[i][1])continue;
                    res+=ok(a,i,j);
            }
        }
        return res;
    }
};
{% endhighlight %}

"3026. Maximum Good Subarray Sum"

prefix sum
using a map to record the minimum value for each a[i]. Whenever we find a value, which is
a[i]-k or a[i]+k, prefix sum will help us find the maximum value.

{% highlight ruby %}
class Solution {
public:
    using ll=long long;
    long long maximumSubarraySum(vector<int>& b, int k) {
        int n=b.size();
        vector<ll> a(n,0);
        vector<ll> pre(n+1,0);
        for(int i=0;i<n;i++) {
            a[i]=b[i];
            pre[i+1]=pre[i]+a[i];
        }
        ll res=LLONG_MIN/2;
        unordered_map<ll,ll> mp;
        for(int i=0;i<n;i++) {
            if(mp.count(a[i]+k)) {
                res=max(res,pre[i+1]-mp[a[i]+k]);
            } 
            if(mp.count(a[i]-k)) {
                res=max(res,pre[i+1]-mp[a[i]-k]);
            }
            if(mp.count(a[i]))
                mp[a[i]]=min(mp[a[i]],pre[i]);
            else 
                mp[a[i]]=pre[i];
        }
        if(res==LLONG_MIN/2) return 0;
        return res;
        
    }
};
{% endhighlight %}

"3027. Find the Number of Ways to Place People II"

{% highlight ruby %}
class Solution {
public:
    using ll=long long;
    int numberOfPairs(vector<vector<int>>& p) {
        int res=0;
        sort(begin(p),end(p),[](auto x,auto y){
            return x[0]<y[0] || (x[0]==y[0] && x[1]>y[1]);
        });
        for(int i=0;i<p.size();i++) {
            int ym=INT_MIN;
            for(int j=i+1;j<p.size();j++) {
                if(p[j][1]>p[i][1]) continue;
                if(p[j][1]>ym) {
                    res++;
                    ym=p[j][1];
                }
            }
        }
        return res;
        
    }
};
{% endhighlight %}
