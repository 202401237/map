### map
contest

qution-1(two sum)
code :-
class Solution {
    public:
        vector<int> twoSum(vector<int>& nums, int target) {
            unordered_map<int,int>m;
            vector<int>v;
            int t;
            for(int i=0;i<nums.size();i++){
                t = target - nums[i];
                if(m.find(t)!=m.end()){
                    v.push_back(i);
                    v.push_back(m[t]);
                    return v;
                }
                else{
                    m[nums[i]] = i;
                }
            }
            return {-1,-1};
        }
    };
qution-2(longestConsecutive )
code :-
class Solution {
    public:
        int longestConsecutive(vector<int>& nums) {
            set<int>s(nums.begin(),nums.end());
            int c=1,m=1;
            if(nums.size()==0) return 0;
            for(auto it = s.begin();it!=s.end();it++){
                
                auto y = it;
                y++;
                if(y==s.end()) break;
                if(*(it) + 1 == *y){
                    c++;
                    m = max(m,c);
                }
                else c=1;
            }
            return m;
        }
    };
qution-3(firstUniqChar)
code :-
class Solution {
    public:
        int firstUniqChar(string s) {
            unordered_map<char,int>m;
            for(int i=0;i<s.size();i++){
                m[s[i]]++;
            }
            for(int i=0;i<s.size();i++){
                if(m[s[i]] == 1) return i;
            }
            return -1;
        }
    };
qution-4(topKFrequent)
code :-    
class Solution {
    public:
        vector<int> topKFrequent(vector<int>& nums, int k) {
           unordered_map<int,int>m;
           vector<int>v(k);
           for(int i=0;i<nums.size();i++){
                m[nums[i]]++;
           } 
           multimap<int,int>f;
           for(auto [p,q] : m){
            f.insert({q,p});
           }
           int i=0;
           for(auto [p,q] : f){
            v[i] = q;
            i++;
            if(i==k) i=0;
           }
           return v;
        }
    };
qution-5(isValidSudoku)
code :-   
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& b) {
        vector<unordered_set<char>> rows(9), cols(9), boxes(9);

        for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++) {
                if(b[i][j] == '.') continue; // Skip empty cells
                
                char curr = b[i][j];
                int boxIndex = (i / 3) * 3 + (j / 3);
                
                if (rows[i].count(curr) || cols[j].count(curr) || boxes[boxIndex].count(curr)) {
                    return false; // Found duplicate
                }

                rows[i].insert(curr);
                cols[j].insert(curr);
                boxes[boxIndex].insert(curr);
            }
        }
        return true; // Sudoku is valid
    }
};
