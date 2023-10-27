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

# 4.Group Anagrams

## using map of key,vecto<string>. generate a key for the strings based on freq. of characters and map those with the strings and push them respectively. 

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        map<string,vector<string>>m;
        vector<vector<string>>op;
        for(int i=0;i<strs.size();i++){
            string key=genKey(strs[i]);
            m[key].push_back(strs[i]);
        }
        for(auto i:m){
            op.push_back(i.second);
        }
        return op;
    }
    string genKey(string s){
        vector<int>v(26,0);
        for(int i=0;i<s.size();i++){
            v[s[i]-'a']++;
        }
        string key;
        for(int i=0;i<v.size();i++){
            key+=(v[i]+'0');
        }
        return key;
    }
};
```

# 5.Top K freq. elements

## 3 steps of finding freq, sorting them desc based on freq, looping first k elements

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int>op;
        map<int,int>m;
        //freq map
        for(int i=0;i<nums.size();i++){
            m[nums[i]]++;
        }
        //sorting desc based on freq count
        vector<pair<int,int>>v;
        for(auto i:m){
            v.push_back(make_pair(i.second,i.first));
        }
        sort(v.rbegin(),v.rend());
        //looping untill k elements
        for(int i=0;i<k;i++){
            op.push_back(v[i].second);
        }
        return op;
    }
};
```

# 6.Product array except self 

## take l and r arrays having products from left and right. get op array from l[i-1]*r[i+1]. this excludes current element.

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int>op;
        vector<int>l;
        vector<int>r;
        int prod=1;
        for(int i=0;i<nums.size();i++){
            l.push_back(prod*nums[i]);
            prod*=nums[i];
        }
        prod=1;
        for(int i=nums.size()-1;i>=0;i--){
            r.push_back(prod*nums[i]);
            prod*=nums[i];
        }

        reverse(r.begin(),r.end());

        for(int i=0;i<nums.size();i++){
            if(i==0) op.push_back(r[1]);
            else if(i==nums.size()-1) op.push_back(l[nums.size()-2]);
            else{
                op.push_back(l[i-1]*r[i+1]);
            }
        }
        return op;
    }
};
```

# 7.Valid Sudokku

## use map for freq of chars. check rowwise - 2 fors, colwise -  2 fors and blockwise - 4 fors

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        for(int i=0;i<9;i++){
            map<char,int> m;
            for(int j=0;j<9;j++){
                if(board[i][j]!='.'){
                    if(m[board[i][j]]==0){
                        m[board[i][j]]++;
                    }else{
                        return false;
                    }
                }
            }
        }
        // check cols
        for(int i=0;i<9;i++){
            map<char,int> m;
            for(int j=0;j<9;j++){
                if(board[j][i]!='.'){
                    if(m[board[j][i]]==0){
                        m[board[j][i]]++;
                    }else{
                        return false;
                    }
                }
            }
        }
        // check boxes 3x3
        for(int i=0;i<9;i+=3){
            for(int j=0;j<9;j+=3){
                map<char,int> m;
                for(int x=i;x<i+3;x++){
                    for(int y=j;y<j+3;y++){
                        if(board[x][y]!='.'){
                            if(m[board[x][y]]==0){
                                m[board[x][y]]++;
                            }else{
                                return false;
                            }
                        }
                    }
                }
            }
        }
        return true;
    }
};

```

# 9.longest consecutive sequence

## using dp on sorted array. 3 conditions

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if(nums.size()==0) return 0;
        vector<int>v(nums.size(),0);
        v[0]=1;
        sort(nums.begin(),nums.end());
        for(int i=1;i<nums.size();i++){
            if(nums[i]==1+nums[i-1]){
                v[i]=1+v[i-1];
            }
            else if(nums[i]==nums[i-1]){
                v[i]=v[i-1];
            }
            else v[i]=1;
        }
        return *max_element(v.begin(),v.end());
    }
};
```

