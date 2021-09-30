---
title: Leetcode
date: 2021-03-25 20:06:26
tags: Leetcode
---

坚持 练习 谨慎<!--more--> 

### 1

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>twos;
        for(int i=0;i<nums.size();i++){
              for(int j=i+1;j<nums.size();j++){
                  if(nums[i]+nums[j]==target){
                      twos.push_back(i);
                      twos .push_back(j);                   
              }
        }
    }
        return twos;
    }
};
    

```

