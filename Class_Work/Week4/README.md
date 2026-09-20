## Programming Techniques Week 4

### Leet Code Easy "217. Contains Duplicates"
[Link](a="https://leetcode.com/problems/contains-duplicate/description/")

#### Problem: 

```
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.
```

#### Solution: 
```cpp
class Solution 
{
public:
    bool containsDuplicate(vector<int>& nums) 
    {
        // Hash set
        unordered_set<int> s;
        for(int i = 0; i < nums.size(); i++)
        {
            // If the set contains the number, it has a duplicate
            if(s.find(nums[i]) != s.end())
                return true;
            // Otherwise, add it to the set
            else
                s.insert(nums[i]);
        }

        // No duplicates were found in the array
        return false;
        
    }
};
```

### Leet Code Medium "1. Two Sum"
[Link](a="https://leetcode.com/problems/two-sum/description/")

#### Problem: 

```
You are given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.
```

#### Solution: 
```cpp
class Solution 
{
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        vector<int> answer;
        unordered_map<int, int> m;

        for(int i = 0; i < nums.size(); i++)
        {
            // What number do we need to reach the target from the number at the current index?
            int need = target - nums[i];

            // Is that number in the map?
            if(m.find(need) != m.end())
            {
                // Prepare and send answer vector 
                answer.push_back(i);
                answer.push_back(m[need]);
                return answer;
            }
            // Otherwise add that number to the map for next iteration
            else
                m[nums[i]] = i;
        }

        return answer;
    }
};
```

### ICPC/Kattis Competition "Streets Ahead"
[Link](a="https://open.kattis.com/problems/streetsahead")

#### Problem:
```
International Connecting Passage Causeway is a long, rutted two-way country road crossed by streets at different points. There are many drivers, and each will drive along the country road starting at some intersection and ending at some other intersection. For each driver, how many intersections will they drive through?

Input:
The first line contains two integers, n (2 ≤ n ≤ 10^5) and q (1 ≤ q ≤ 10^5), where n is the number of cross streets and q is the number of drivers. Each of the next n lines contains a string of at most ten lowercase letters representing the name of one of the streets that crosses the country road. All street names are unique. Driving along the country road in some direction, one sees these streets in exactly the order provided. Each of the next q lines contains two strings of at most ten lowercase letters representing the start and end intersection for each driver. Queries will be between distinct streets.

Output: 
Output q lines, the ith line containing the number of intersections that the ith driver drives through.
```
Example Input:
```
3 3
first
second
third
first second
third first
second third
```
Example Output:
```
0
1
0
```

#### In-Class Solution
This solution works to the above problem and was produced in real-time under the pressure of competition. 

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
	// Variables
    unordered_map<string, int> street_map;
    int n, q;
    string temp, start, end;
    
	// Get initial variable values and setup ordered array
    cin >> n >> q;
    string street_arr[n];
	
	// For each street
    for(int i = 0; i < n; i++)
    {
		// Get it's name, add it to the ordered array, and add the array index to map
        cin >> temp;
        street_arr[i] = temp;
        street_map[temp] = i;
    }
    
	// For each driver
    for(int i = 0; i < q; i++)
    {
		// Get start and end streets
        cin >> start >> end;
		
		// Subtract end street index from start street index
		// Take absolute value because they can go both ways on the road
		// Subtract 1 for 0-indexed arrays
        cout << abs(street_map[end] - street_map[start]) - 1 << endl;
        
    }
}
```