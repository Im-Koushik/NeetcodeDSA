# 1.Contain duplicate or not in an array
## using set approach O(n)

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int>s;
        for(int i=0;i<nums.size();i++){
            if(s.find(nums[i])==s.end()) s.insert(nums[i]);
            else return true;
        }
        return false;
    }
};
```

# 2.Valid Anagrams 
## using sorting and equaling O(n log n) or using maps for counting freq and subtracting freq method O(n)

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        if(s==t) return true;
        return false;
    }
};
```

# 3.2 Sum Problem 
## using linear parsing O(n2)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>res;
        for(int i=0;i<nums.size();i++){
            for(int j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                    res.push_back(i);
                    res.push_back(j);
                    break;
                }
            }
        }
        return res;
    }
};
```

# 4.
