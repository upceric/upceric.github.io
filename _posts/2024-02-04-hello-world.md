---
layout: post
title:  "leetcode biweekly contest 123"
date:   2024-02-04 13:17:11 +0100
categories: jekyll update
---
3024. Type of Triangle II

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

3025. Find the Number of Ways to Place People I
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
