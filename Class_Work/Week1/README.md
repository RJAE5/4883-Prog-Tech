## Programming Techniques Week 1

### ICPC/Kattis Competition "Sun and Moon"
[Link](a="https://open.kattis.com/problems/sunandmoon")

#### Problem:
```
John is a student working as a part-time barista at the micro kitchen of his school department. He operates the espresso machine at the kitchen to make espresso and latte for students seeking energy to study.
Today, there are n students coming to the micro kitchen to place an order. An order is noted with an espresso shot number x ranging between 1 and 4, and an optional letter L that indicates that the student wants to have a x-shot latte. For example, an order 2 means a 2-shot espresso, and an order 3L means a 3-shot latte. Making an x-shot espresso consumes x ounces of water. Making a latte requires steaming milk and consumes one additional ounce of water, e.g. making a 3-shot latte consumes 4 ounces of water. The espresso machine at the micro kitchen has a water tank of s ounces that is full at the beginning of the day. John refills the water tank to s ounces whenever the remaining water in the tank is not enough to fulfill the next student’s order. John fulfills the n orders one by one without changing their order. How many times do John have to refill the water tank today in order to serve all the n students?

Input:
The first line of input has two integers n (1 ≤ n ≤ 100) and s (10 ≤ s ≤ 200). The next n lines each contain a digit between 1 and 4 followed by an optional letter L to describe an order. The orders are to be fulfilled in the given order as they appear in the input.

Output:
Output the number of times John has to refill the water tank of the espresso machine.
```
Example Input:
```
8 10
1
2L
3
4
3L
1
1L
4L
```
Example Output:
```
2
```

#### In-Class Solution (Winner)
This solution works to the above problem and was produced in real-time under the pressure of competition. 
For this particular problem, my team was the first to solve the problem.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    // Variables
    string order;
    int filled = 0;
    int tank; 

    int num_order, max_tank;
    cin >> num_order >> max_tank;
    tank = max_tank;

    // Main loop
    for(int i = 0; i < num_order; i++)
    {
        // Check number of ounces, adding one if it's a latte
        cin >> order;
        int oz = order[0] - '0';
        if(order[1] == 'L')
            oz++;
            
        // Check if tank needs filling
        if(tank < oz)
        {
            tank = max_tank;
            filled++;
        }
        
        // Subtract ounces from tank
        tank -= oz;
    }
    
    // Once loop is complete, cout the number of times it was filled
    cout << filled;
}
```