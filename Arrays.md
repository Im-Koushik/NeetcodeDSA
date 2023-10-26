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

