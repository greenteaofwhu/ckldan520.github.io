# 3.Longest Substring Without Repeating Characters #
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

题意：输出字符串最长无重复字符子串长度。

思路：只需要记录两个相同字符间字符串的长度，取最长的长度返回即可（如果一直到字符串尾端一直未出现此重复字符，便返回此长度）。

实现：建立哈希字符映射，遍历字符串，每次读入一个字符，**并记录此字符首次读入的位置start**，如果后面在下标i位置出现了之前出现过的字符，更新maxlen=max(maxlen,i-start)

		int lengthOfLongestSubstring(string s) {
		        vector<int> dict(256, -1);
		        int maxLen = 0, start = -1;
		        for (int i = 0; i != s.length(); i++) {
		            if (dict[s[i]] > start)
		                start = dict[s[i]];
		            dict[s[i]] = i;
		            maxLen = max(maxLen, i - start);
		        }
		        return maxLen;
		    }