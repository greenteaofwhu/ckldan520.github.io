LeetCode 

1. Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

题意：找到数组中两个元素之和的结果等于给定的数字,返回这两个元素的下标

思路1：两层for循环遍历数组，时间复杂度O(n^2)
<pre> 
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> v;
		int flag = 0;
		for(int i = 0;i < nums.size();i++)
		{
			for(int j = i+1;j < nums.size();j++)
			{
				if(nums[i]+nums[j] == target)
				{
					v.push_back(i);
					v.push_back(j);
					flag = 1;
					break;
				}	
			}
			if(flag)
			break;
		}
		return v;
    }
};
</pre>
思路2：将数组元素映射到哈希表中，然后对于每一个元素值key计算target-key的差值d，然后在哈希表中查找是否存在此差值，
如果存在则返回其下标，时间复杂度O(n)，空间复杂度O(n)。

注意：题目限制了每个元素不能使用两次，因此不能直接进行哈希映射，在每次读入一个元素num[i]和其下标i时，先计算差值d，
然后在之前生成的哈希表中查找此差值，找到了首先将差值元素下标添入返回容器v中，然后再将元素i添入返回容器v中；若未能此前哈希表中查找到差值元素，
将读入的元素nums[i]和下标i读入哈希表中，继续查找。
<pre>
vector<int> twoSum(vector<int> &numbers, int target)
{
    //Key is the number and value is its index in the vector.
	unordered_map<int, int> hash;
	vector<int> result;
	for (int i = 0; i < numbers.size(); i++) {
		int numberToFind = target - numbers[i];

            //if numberToFind is found in map, return them
		if (hash.find(numberToFind) != hash.end()) {
                    //+1 because indices are NOT zero based
			result.push_back(hash[numberToFind]);
			result.push_back(i);			
			return result;
		}

            //number was not found. Put it in the map.
		hash[numbers[i]] = i;
	}
	return result;
}
</pre>