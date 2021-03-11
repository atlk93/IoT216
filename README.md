# IoT216


2021/03/11

```
// Project1.cpp : 이 파일에는 'main' 함수가 포함됩니다. 거기서 프로그램 실행이 시작되고 종료됩니다.
//

#include <iostream>
#include <stdio.h>
#include <cmath>

class Point {
public:
    Point(int a, int b) {
        x = a;
        y = b;
    }
    ~Point() { delete ppp; }
private:
    int* ppp;
public:
    int x;
    int y;

    int* Pointfunc() {
        ppp = (int*)malloc(1000);
        return ppp;
    }

};

class Rect {
private:
public:
    /* Rect(int x1, int y1, int x2, int y2 Point pp1, Point pp2) {
         p1.x = pp1.x;
         p1.y = pp1.y;
         p2.x = pp2.x;
         p2.y = pp2.y;
         p13.x = pp1.x;
         p13.y= pp2.y;
     }*/
    Point p1;
    Point p2;
    Point p13;

    int area() {//X*Y : 두 점으로 이루어진 사각형의 넓이
        int x = p2.x - p1.x;
        int y = p2.y - p1.y;
        return x * y;
    }

    //distance: 두 점간의 거리
    double distance();
    /*   int xx = abs(p2.x - p1.x);
       int yy = abs(p2.y - p1.y);
       return sqrt(xx * xx + yy * yy);
   }*/

    int tlength();
};

class RectEx :Rect {
    Point p3 = { p1.x, p2.y };
    Point p4 = { p2.x, p1.y };
public:
    int tLength() {
        int x = abs(p1.x - p2.x);
        int y = abs(p1.y - p2.y);
        return (2 * x + 2 * y);

    }
};



double Rect::distance() {
    int xx = abs(p2.x - p1.x);
    int yy = abs(p2.y - p1.y);
    return sqrt(xx * xx + yy * yy);
}

int main()
{
    std::cout << "Hello World!\n";
    printf("이것은 printf에서 내보낸 문자열입니다. \n");
    Point p1(10, 10), p2(20, 20);
    /*Rect r1 = { p1, p2 };*/
    /*RectEx r2 = { {10,10},{20,20} };*/
   /* r1.p1.x = 15;
    r1.p1.y = 15;*/
    // printf("두 점 p1(%d, %d), p2(%d, %d)로 구성되는 사각의 면적은 %d입니다.\n",r1.p1.x, r1.p1.y, r1.p2.x, r1.p2.y, r1.area());
     //printf("두점간의 거리는 %.2f입니다.\n",r1.distance());
     //printf("사각형의 전체 둘레길이는 %d입니다.\n", r2.tLength());
}
```
