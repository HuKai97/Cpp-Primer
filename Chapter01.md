# 1.2、初始输入输出

## Exercise1.3
编写程序，在标准输出上打印Hello, World.
```c
#include <iostream>

int main()
{
    std::cout << "Hello, World" << std::endl;
    return 0;
}
```

## Exercise1.4
编写程序使用乘法运算符*，来打印两个数的乘积.
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of " << v1 << " and " << v2 << " is " << v1 * v2 << std::endl;
    return 0;
}
```

## Exercise1.5
将上面的程序重写，将每个运算对象的打印操作放在一条独立的语句中。
```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of ";
    std::cout << v1;
    std::cout << " and ";
    std::cout << v2;
    std::cout << " is ";
    std::cout << v1 * v2 << std::endl;
    return 0;
}
```

## Exercise1.6
判断下面程序哪里错了？  
error: expected primary-expression before '<<' token   
“<<”符号左右两边必须有两个对象，且左边必须是输出流对象cout。
```cpp
std::cout << "The product of " << v1;
          << " and " << v2;
          << " is " << v1 * v2 << std::endl;
```

# 1.4.1-1.4.2、while语句和for语句
## Exercise1.9
编写程序，使用while循环从50加到100.
```cpp
#include <iostream>

int main()
{
    int sum = 0, start = 50, end = 100;
    while(start <= end)
    {
        sum += start;
        start++;
    }
    std::cout << "sum of 50 to 100 is " << sum << std::endl;
    return 0;
}
```

## Exercise1.10
编写程序，使用--递减符号在循环中实现按递减顺序打印出10到0之间的整数.
```cpp
#include <iostream>

int main()
{
    for(int start = 10, end = 0; start >= end; start--)
    {
        std::cout << start << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

## Exercise1.11
输出两个整数，打印这两个整数之间的所有整数。
```cpp
#include <iostream>

void print_start_to_end(int start, int end)
{
    if(start > end)
    {
        print_start_to_end(end, start);
        return;
    }
    for(int i = start; i <= end; i++)
    {
        std::cout << i << " ";
    }
}

int main()
{
    int start = 0, end = 0;
    std::cout << "input two number: " << std::endl;
    std::cin >> start >> end;
    print_start_to_end(start, end);
    return 0;
}
```

# 1.4.3、读取数量不定的输入数据
## Exercise1.16
编写程序，从cin读取一组数，输出其和。
```cpp
#include <iostream>

int main()
{
    int sum = 0;
    for(int val; std::cin >> val; sum += val);
    std::cout << sum << std::endl;
    return 0;
}
```
# 1.4.4、if语句
## Exercise1.17-18
例子：统计输入数组中每个字符出现的次数。
```cpp
#include <iostream>

int main()
{
    int curVal = 0, val = 0;
    if (std::cin >> curVal){
        int count = 1;
        while (std::cin >> val){
            if (val == curVal) ++count;
            else{
                std::cout << curVal << " occur " << count << " times." << std::endl;
                curVal = val;
                count = 1;
            }
        }
        std::cout << curVal << " occur " << count << " times." << std::endl;
    }
    return 0;
}
```

## Exercise1.19
编写程序，实现输入两个数，打印这两个数之间的整数，且能够处理第一个数比第一个数大的情况。
```cpp
#include <iostream>

int main()
{
    int small = 0, big = 0;
    std::cin >> small >> big;
    if (small > big){
        int temp = big;
        big = small;
        small = temp;
    }
    while (small <= big){
        std::cout << small << " ";
        small += 1;
    }
    std::cout << std::endl;
    return 0;
}
```


# 1.5、类

## Exercise1.20
编写程序：读取一组书籍销售记录，将每条记录打印到标准输出上。

```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    // 0-201-78345-x 3 20.00
    // for(Sales_item item; std::cin >> item; std::cout << item << std::endl);
    Sales_item item;
    while (std::cin >> item){
        std::cout << item << std::endl;
    }
    return 0;
}
```

## Exercise1.21
编写程序，读取两个ISBN相同的Sales_item对象，输出它们的和。
```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    // 1
    // 0-201-78345-x 3 20.00 + 0-201-78346-x 2 10.00 -> 0-201-78345-x 5 80 16
    // Sales_item item1, item2;
    // std::cin >> item1 >> item2;
    // std::cout << item1 + item2 << std::endl;

    // 2
    // 0-201-78346-x 2 10.00 + 0-201-78346-x 3 25.00 -> 0-201-78346-x 5 95 19
    // 0-201-78345-x 3 20.00 + 0-201-78346-x 2 10.00 -> Different ISBN
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    if (item1.isbn() == item2.isbn()){
        std::cout << item1 + item2 << std::endl; 
    }else{
        std::cerr << "Different ISBN" << std::endl;
    }
    return 0;
}
```

## Exercise1.22
编写程序，读取多个具有相同ISBN的销售记录，输出所有记录的和。】
```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    // 0-201-78346-x 2 10.00 + 0-201-78346-x 2 20.00 + 0-201-78346-x 2 30.00 -> 0-201-78346-x 6 120 20
    Sales_item total;
    if (std::cin >> total){
        Sales_item item;
        while (std::cin >> item){
            if (item.isbn() == total.isbn()){
                total += item;
            }else{
                std::cerr << "Different ISBN" << std::endl;
                return -1;
            }
        }
        std::cout << total << std::endl;
    }else{
        std::cerr << "No Data" << std::endl;
    }
    return 0;
}
```



## Exercise1.23-1.24
编写程序，读取多条销售记录，并统计每个ISBN（每本书）有几条销售记录。   
测试数据：data/book.txt

```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    Sales_item curItem, valItem;
    if (std::cin >> curItem){
        int count = 1;
        while (std::cin >> valItem){
            if (curItem.isbn() == valItem.isbn()){
                count++;
            }else{
                std::cout << curItem << ", occurs " << count << " times." << std::endl;
                curItem = valItem;
                count = 1;
            }
        }
        std::cout << curItem << ", occurs " << count << " times." << std::endl;
    }
    return 0;
}
```
## Exercise1.25
测试数据：data/book.txt
```cpp
#include <iostream>
#include "include/Sales_item.h"

int main()
{
    Sales_item totalItem;
    if (std::cin >> totalItem){
        Sales_item curItem;
        while (std::cin >> curItem){
            if (curItem.isbn() == totalItem.isbn()){
                totalItem += curItem;
            }else{
                std::cout << totalItem << std::endl;
                totalItem = curItem;
            }
        } 
        std::cout << totalItem << std::endl;
    }else{
        std::cerr << "Not Data" << std::endl;
        return -1;
    }
    return 0;
}
```