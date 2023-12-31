# Leetcode 56. Merge Intervals

## 题目描述
<div class="_1l1MA" data-track-load="description_content"><p>Given an array&nbsp;of <code>intervals</code>&nbsp;where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return <em>an array of the non-overlapping intervals that cover all the intervals in the input</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,3],[2,6],[8,10],[15,18]]
<strong>Output:</strong> [[1,6],[8,10],[15,18]]
<strong>Explanation:</strong> Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,4],[4,5]]
<strong>Output:</strong> [[1,5]]
<strong>Explanation:</strong> Intervals [1,4] and [4,5] are considered overlapping.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= intervals.length &lt;= 10<sup>4</sup></code></li>
	<li><code>intervals[i].length == 2</code></li>
	<li><code>0 &lt;= start<sub>i</sub> &lt;= end<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

## 测试用例
* 无效输入测试用例（输入数组为空；长度为n的数组中包含 0 到 n-1之外的数字）
```
[[1,3],[2,6],[8,10],[15,18]]
[[1,4],[4,5]]
```

## 代码
## 解法一 72% 96%
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        const int START=0, END=1;   
        
        vector< vector<int> > result;
    
        sort( intervals.begin(), intervals.end() );
        
        for( auto const &curInterval : intervals ){
            if ( (result.size() == 0 ) || (result.back()[END] < curInterval[START] ) ){
                result.push_back( curInterval );
            }else{
                result.back()[END] = max( result.back()[END], curInterval[END] );
            }
        }
        
        return result;
    }
};
```
