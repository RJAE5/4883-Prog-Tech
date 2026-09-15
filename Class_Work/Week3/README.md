## Programming Techniques Week 3

### Leet Code Easy "191. Number of 1 Bits"
[Link](a="https://leetcode.com/problems/number-of-1-bits/description/")

#### Problem: 

```
Given a positive integer n, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).
```

#### Solution: 
```cpp
class Solution 
{
public:
    int hammingWeight(int n) 
    {
        // Counter variable
        int setBits = 0;

        // While nonzero bits remain
        while(n > 0)
        {
            // Check least significant bit to see if 1
            if(n % 2 == 1)
            {
                // Increase counter if so
                setBits++;
            }

            // Truncate n's least signifcant bit
            n /= 2;
        }

        return setBits;
        
    }
};
```

### ICPC/Kattis Competition "Ultimate Binary Watch"
[Link](a="https://open.kattis.com/problems/ultimatebinarywatch")

#### Problem:
```
The Ultimate Binary Watch is a maker project that uses small LEDs to display time on a watch face. The display uses four columns of four LEDs each, with each column representing one digit of the current time in hours and minutes. Time is displayed in 24-hour format, with the 1st (left-most) column displaying the tens position for hours, the 2nd column displaying the ones position for hours, the 3rd column displaying the tens position for minutes, and the last (rightmost) column displaying the ones position for minutes. The bottom LED of each column shows the lowest-order bit of its represented digit, with the bit positions increasing moving up the column. For example, the time 1615 would be displayed as shown in the figure. Write a program that will take a 24-hour time and print the corresponding watch face.
```
Example Output for `1615`:
```
. .  . .
. *  . *
. *  . .
* .  * *
```

#### In-Class Solution (Winner)
This solution works to the above problem and was produced in real-time under the pressure of competition. 
For this particular problem, my team was the first to solve the problem, though the code was not as clean as it could be.
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int timeRaw;
    cin >> timeRaw;
    
    int hourTens, hourOnes, minTens, minOnes;
    string hourTensBin, hourOnesBin, minTensBin, minOnesBin;
    
    minOnes = timeRaw % 10;
    minTens = (timeRaw / 10) % 10;
    hourOnes = (timeRaw / 100) % 10;
    hourTens = (timeRaw / 1000);
        
    minOnesBin = "....";
    
    for(int i = 3; minOnes > 0; i--)
    {
        if( minOnes % 2 == 1)
        {
            minOnesBin[i] = '*';
            
        }
        else
        {
            minOnesBin[i] = '.';
        }
        minOnes /= 2;

    }
        
    minTensBin = "....";
    
    for(int i = 3; minTens > 0; i--)
    {
        if( minTens % 2 == 1)
        {
            minTensBin[i] = '*';
        }
        else
        {
            minTensBin[i] = '.';
        }
        minTens /= 2;

    }
        
    hourOnesBin = "....";
    
    for(int i = 3; hourOnes > 0; i--)
    {
        if( hourOnes % 2 == 1)
        {
            hourOnesBin[i] = '*';
        }
        else
        {
            hourOnesBin[i] = '.';
        }
        hourOnes /= 2;

    }
    
        hourTensBin = "....";
    
    for(int i = 3; hourTens > 0; i--)
    {
        if( hourTens % 2 == 1)
        {
            hourTensBin[i] = '*';
        }
        else
        {
            hourTensBin[i] = '.';
        }
        hourTens /= 2;

    }
    
    for(int i = 0; i < 4; i++)
    {
        cout << hourTensBin[i] << " " << hourOnesBin[i] << "   "
             << minTensBin[i] << " " << minOnesBin[i] << endl;
    }
    
}
```

#### Cleaner Solution
This solution is adapted from the original in-class work to be cleaner, more concise, and with improved readability 
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    // Variables
    int timeRaw, hourTens, hourOnes, minTens, minOnes;
    cin >> timeRaw;

    // Initialized for all 
    string hourTensBin = "....";
    string hourOnesBin = "....";
    string minTensBin = "....";
    string minOnesBin = "....";
    
    // Extract time positions
    minOnes = timeRaw % 10;
    minTens = (timeRaw / 10) % 10;
    hourOnes = (timeRaw / 100) % 10;
    hourTens = (timeRaw / 1000);

    // For each number position, check least significant bit (LSB)
    // If 1, set LSB string position to 1, represented by '*'
    // Else, set LSB string position to 0, represented by '.'
    // Divide all time position variables by 2 to truncate LSB
    for(int i = 3; i >= 0; i--)
    {
        if(minOnes % 2 == 1) minOnesBin[i] = '*';

        if(minTens % 2 == 1) minTensBin[i] = '*';

        if(hourOnes % 2 == 1) hourOnesBin[i] = '*';

        if(hourTens % 2 == 1) hourTensBin[i] = '*';

        hourTens /= 2;
        hourOnes /= 2;
        minTens /= 2;
        minOnes /= 2;
    }
    
    // Formatted output corresponding to requirements
    for(int i = 0; i < 4; i++)
    {
        cout << hourTensBin[i] << " " << hourOnesBin[i] << "   "
             << minTensBin[i] << " " << minOnesBin[i] << endl;
    }
    
}
```
> Technically, the second `for` loop is not necessary, we could `cout` the positions as they are checked, but that would require some more logic to deal with the reversing, and I think it helps for readability to leave as is.
