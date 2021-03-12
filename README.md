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

2021/03/12
```
#include <iostream>

class Point // 기본적으로 private : 외부 참조 불가
{
public:		// : 외부 참조 가능
	int x, y;
	Point(int a, int b) : x(a), y(b) {}
	//{
	//	x = a; y = b;
	//}
	Point() {} // null 생성자

	int GetX() { return x; }
	int GetY() { return y; }

	void SetX(int a) { x = a; }
	void SetY(int a) { y = a; }

	//	p1 = p + n;		p1,p:Point		n:int	===>	p1.x = p.x + n;		p1.y = p.y + n;
	Point operator+(int n)
	{
		Point p1;
		p1.x = x + n; p1.y = y + n;
		return p1;
	}
	Point operator+(Point p)
	{
		Point p1;
		p1.x = x + p.x;	p1.y = y + p.y;
		return p1;
	}
};

class Rect
{
private:
	Point p1, p2;
public:
	Rect(Point pp1, Point pp2) : p1(pp1), p2(pp2)
	{
		//		p1 = pp1; p2 = pp2; // class 변수의 대입문
	}

	Rect() : p1(0, 0), p2(0, 0) {}
	// Rect(Point& pp1, Point& pp2)

	void SetP1(Point p) { p1 = p; }
	void SetP2(Point p) { p2 = p; }

	int GetX() { return abs(p1.x - p2.x); }
	int GetY() { return abs(p1.y - p2.y); }
	int area()
	{
		int x = p1.x - p2.x;
		int y = p1.y - p2.y;

		return abs(x * y);
	}
};

// Point 클래스와 Rect 클래스는 은닉되어 있음.

// 공개된 정보는 Point 생성자와 Rect 생성자가 알려져 있음.

// Rect 클래스에는 사각형의 면적을 구하는 area 함수가 존재

//

// ---> Rect의 대각선 길이를 구하는 Distance 함수가 필요함

// dist = sqrt(x*x + y*y)

class RectEx : public Rect // Rect class를 상속 private
{
int a;
public:
	RectEx(Point pp1, Point pp2, int a) : Rect(pp1, pp2)
	{
		//SetP1(pp1); SetP2(pp2);
	}
	double Distance()
	{
		int x = GetX();
		int y = GetY();

		return sqrt(x * x + y * y);
	}
};



// Mission : Circle 클래스를 정의하고 멤버 함수를 구현하세요.

// Member Function : 지름(diameter), 원둘레(CLen), 원면적(area)

// *** 단, Rect 클래스를 상속받아서 구현 ***

//	Rect의 두 점을 지름으로 하는 원(Circle)의 정의

#define PI 3.14159265
class Circle : public Rect
{
private:
	Point cp;
	double rad;
public:
	Circle(Point pp1, Point pp2) : Rect(pp1, pp2), cp(0, 0), rad(0)
	{
		cp.SetX((pp1.x + pp2.x) / 2);
		cp.SetY((pp1.y + pp2.y) / 2);

		int x = GetX();
		int y = GetY();

		rad = sqrt(x * x + y * y) / 2;
	}

	double dia()
	{
		return rad * 2;
	}

	double CLen()
	{
		return dia() * PI;
	}

	double area()
	{
		return rad * rad * PI;
	}
};





int func1(Rect* r);
int func2(Rect& r);
int func3(Circle& c);

int main()
{
	int n1 = 10, n2 = 20;

	Point p1(n1, n1), p2(n2, n2);
	//	Rect r1 = { {10,10},{20,20} }; // struct type 초기화
	Rect r1(p1, p2);	// Rect class 생성자 이용 초기화
	Rect r2;

	Circle c1(p1, p2);

	func1(&r1); // 포인트 변수 전달을 위해 변수(클래스)의 주소 전달

	func2(r1);	// 레퍼런스 타입은 그냥 변수명 전달


	printf("여기는 main입니다 :\n두 점 p1(10,10)과 p2(20,20)으로 이루어진 사각형의 면적은 %d입니다\n", r2.area());

	func3(c1);

	p1.SetX(15); p1.SetY(15);
	Point p3 = p1 + 10;	// p3(25,25)	
	printf("Point 클래스의 연산자 오버로딩 테스트 (+) : p1(%d,%d)+%d ---> (%d,%d)\n",p1.x,p1.y,10,p3.x,p3.y);

	Point p4 = p1 + p3;
	Point* p5 = &p4;
	printf("Point 클래스의 연산자 오버로딩 테스트 (+) : p1(%d,%d)+p3(%d,%d)---> (%d,%d)\n", p1.x, p1.y, p3.x, p3.y, p4.x, p4.y);
	printf("Point 클래스의 연산자 오버로딩 테스트 (+) : p1(%d,%d)+p3(%d,%d)---> (%d,%d)\n", p1.x, p1.y, p3.x, p3.y, p5->x, p5->y);
}

int func1(Rect* r1)
{
	printf("두 점 p1(10,10)과 p2(20,20)으로 이루어진 사각형의 면적은 %d입니다\n", r1->area());

	return 0;
}

int func2(Rect& r1)
{
	printf("두 점 p1(10,10)과 p2(20,20)으로 이루어진 사각형의 면적은 %d입니다\n", r1.area());

	return 0;
}

int func3(Circle& c1)
{
	printf("두 점 p1(10,10)과 p2(20,20)를 지나는 원의 면적은 %f입니다\n", c1.area());
	printf("두 점 p1(10,10)과 p2(20,20)를 지나는 원의 지름은 %f입니다\n", c1.dia());
	printf("두 점 p1(10,10)과 p2(20,20)를 지나는 원의 둘레는 %f입니다\n", c1.CLen());

	return 0;
}
```
