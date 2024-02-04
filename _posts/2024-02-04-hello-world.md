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

