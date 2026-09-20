## Programming Techniques Week 2

### Leet Code Easy "2582. Pass the Pillow"
[Link](a="https://leetcode.com/problems/pass-the-pillow/description/")

#### Problem: 

```
There are n people standing in a line labeled from 1 to n. The first person in the line is holding a pillow initially. Every second, the person holding the pillow passes it to the next person standing in the line. Once the pillow reaches the end of the line, the direction changes, and people continue passing the pillow in the opposite direction.

For example, once the pillow reaches the nth person they pass it to the n - 1th person, then to the n - 2th person and so on.
Given the two positive integers n and time, return the index of the person holding the pillow after time seconds.
```

#### Solution: 
```cpp
class Solution 
{
public:
    int passThePillow(int n, int time) 
    {
        int remaining = time % (2 * (n-1));

        if(remaining < n)
        {
            return 1 + remaining;
        }
        else
        {
            // Account for all of the forward steps
            remaining -= n;
            return (n - 1) - remaining;
        }
    }
};
```

### Leet Code Medium "1823. Find the Winner of the Circular Game"
[Link](a="https://leetcode.com/problems/find-the-winner-of-the-circular-game/description/")

#### Problem: 

```
There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

1. Start at the 1st friend.
2. Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
3. The last friend you counted leaves the circle and loses the game.
4. If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
5. Else, the last friend in the circle wins the game.

Given the number of friends, n, and an integer k, return the winner of the game.
```

#### Solution: 
```cpp
class Solution 
{
public:
    int findTheWinner(int n, int k) 
    {
        queue <int> q;

        for(int i = 1; i <= n; i++)
        {
            q.push(i);
        }
        
        while(q.size() > 1)
        {
            // Cycle through all full cycles
            int loser = (k - 1) % q.size();

            for(int i = 0; i < loser; i++)
            {
                // Cycle through remaining steps
                q.push(q.front());
                q.pop();
            }

            q.pop();
        }

        return q.front();
        

    }
};
```

### ICPC/Kattis Competition "Sun and Moon"
[Link](a="https://open.kattis.com/problems/sunandmoon")

#### Problem:
```
You recently missed an eclipse and are waiting for the next one! To see any eclipse from your home, the sun and the moon must be in alignment at specific positions. You know how many years ago the sun was in the right position, and how many years it takes for it to get back to that position. You know the same for the moon. When will you see the next eclipse? 

Input:
The input consists of two lines. The first line contains two integers, ds and ys (0 ≤ ds < ys ≤ 50), where ds is how many years ago the sun was in the right position, and ys is how many years it takes for the sun to be back in that position. The second line contains two integers, dm and ym (0 ≤ dm < ym ≤ 50), where dm is how many years ago the moon was in the right position, and ym is how many years it takes for the moon to be back in that position. 

Output: 
Output a single integer, the number of years until the next eclipse. The data will be set in such a way that there is not an eclipse happening right now and there will be an eclipse within the next 5,000 years.
```
Example Input:
```
3 10
1 2
```
Example Output:
```
7
```

#### In-Class Solution
This solution works to the above problem and was produced in real-time under the pressure of competition. 

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Variables and input
    int ds, ys, dm, ym;
    
    cin >> ds >> ys;
    cin >> dm >> ym;
    
    // Constant for loop, looping through years
    for(int i = 1; i < 5000; i++)
    {
        // If moon is in the right position
        if((dm + i) % ym == 0)
        {
            // If sun is in the right position
            if((ds + i) % ys == 0)
            {
                // Cout years passed and end program
                cout << i;
                return 0;
            
            }
        }
    }
}
```