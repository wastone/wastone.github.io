---
title: 一个简单算法的改进
date: 2017-09-25 15:10:46
comments: true
reward: true
tags: [算法,随笔]
---

>算法

最近看到一个经常做的一个算法题，``判断一个数是不是素数?``，素数的概念是``在大于1的自然数中，只能被1和其本身整除的数成为质数，也是常说的素数``，按照这个概念，我们常见得算法有：
<!-- more -->
```
//方法一
function isPrime_1(num){
    if(isNaN(num) || num <= 1){
        return false;
    }
    var tmp = num - 1;
    for(var i = 2;i <= tmp; i++){
        if(num % i == 0){
            return false;
        }
    }
    return true;
}


//方法二   根据方法一改进  主要用到Math的sqrt方法筛选掉一部分 增加效率
function isPrime_2(num){
    if(isNaN(num) || num <= 1){
        return false;
    }
    var tmp = Math.sqrt(num);
    for(var i = 2;i <= tmp; i++){
        if(num % i == 0){
            return false;
        }
    }
    return true;
}
```
后面有人发现了一个更快速的判断方法：
首先看一个关于质数分布的规律：大于等于5的质数一定和6的倍数相邻。例如5和7，11和13,17和19等等；
证明：令x≥1，将大于等于5的自然数表示如下：
```
······ 6x-1，6x，6x+1，6x+2，6x+3，6x+4，6x+5，6(x+1），6(x+1)+1 ······
```
可以看到，不在6的倍数两侧，即6x两侧的数为``6x+2，6x+3，6x+4``，由于``2(3x+1)，3(2x+1)，2(3x+2)``，所以它们一定不是素数，再除去6x本身，显然，素数要出现只可能出现在6x的相邻两侧。这里有个题外话，关于孪生素数，有兴趣的道友可以再另行了解一下，由于与我们主题无关，暂且跳过。这里要注意的一点是，在6的倍数相邻两侧并不是一定就是质数。
根据以上规律，判断质数可以6个为单元快进，即将方法（2）循环中``i++``步长加大为6，加快判断速度，代码如下：
```
//方法三
function isPrime_3(num){
    if(isNaN(num) || num <= 1){
        return false;
    }
    if(num == 2 || num == 3){
        return true;
    }
    if(num % 6 != 1&&num % 6 != 5){
        return false;
    }
    var tmp = Math.sqrt(num);
    for(var i = 2;i <= tmp; i++){
        if(num % i == 0){
            return false;
        }
    }
    return true;
}
```

[参考：huang_miao_xin的博客](http://blog.csdn.net/huang_miao_xin/article/details/51331710)
