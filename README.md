# ADD 2 num
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n=nums.size();
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if(nums[i]+nums[j]==(target)){
                    vector <int> arr(2);
                arr[0]=i;
                 arr[1]=j;
                    return arr;
            }}}
      return {}; }
        
        
    
};

