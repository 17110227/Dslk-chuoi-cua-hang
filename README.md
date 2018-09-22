
#include "pch.h"
#include <iostream>
using namespace std;
typedef struct mathang                //Lưu tên các mặt hàng có trong chuỗi cửa hàng và giá tiền
{
	char ten[100];
	int giatien;
	char mamh[8];
}MH;
typedef struct NodeMH
{
	MH Info;
	NodeMH *pNext;
};
typedef struct MHnode
{
	NodeMH *pHead;
	NodeMH *pTail;
};
//Hàm tạo danh sách
void CreateList(MHnode &l);
//Hàm tạo 1 phần tử của danh sách
NodeMH *GetNode(MH a);
//Hàm thêm đầu, cuối của danh sách
void AddHead(MHnode &L, NodeMH *p);
void AddTail(MHnode &L, NodeMH *p);
//Hàm nhập, in thông tin của mỗi mặt hàng
void nhapmathang(MH &a);
void inmathang(MH a);
//Hàm nhập xuất danh sách
void nhap(MHnode &l, int n);  
void xuat(MHnode &l);
int main()
{
	MH a[100];
	int n;
	cout << "Nhap so mat hang can quan li: ";
	cin >> n;
	MHnode L;
	CreateList(L);
	nhap(L, n);
	xuat(L);
}
void nhapmathang(MH &a)
{
	cout << "Nhap ten mat hang: ";
	cin.ignore();
	cin.getline(a.ten, 9);
	cout << "Nhap gia tien: ";
	cin >> a.giatien;
	cout << "Nhap ma mat hang: ";
	cin >> a.mamh;	
}
void inmathang(MH a)
{
	cout << endl;
	cout << "Ma so mat hang la: " << a.mamh << endl;
	cout << "Ten mat hang: " << a.ten << endl;
	cout << "Gia tien la: " << a.giatien << endl;
	cout << endl;
}
void xuat(MHnode &l)
{
	NodeMH *p;
	p = l.pHead;
	while (p != NULL)
	{
		inmathang(p->Info);
		p = p->pNext;
	}
}
void CreateList(MHnode &l)
{
	l.pHead = l.pTail = NULL;
}
void AddHead(MHnode &L, NodeMH *p)
{
	if (L.pHead == NULL)
	{
		L.pHead = L.pTail = p;
	}
	else
	{
		p->pNext = L.pHead;
		L.pHead = p;
	}
}
void AddTail(MHnode &L, NodeMH *p)
{
	if (L.pHead == NULL)
	{
		L.pHead = L.pTail = p;
	}
	else
	{
		L.pTail->pNext = p;
		L.pTail = p;
	}
}
NodeMH *GetNode(MH a)
{
	NodeMH *p = new NodeMH;
	if (p == NULL)
	{
		return NULL;
	}
	p->Info = a;
	p->pNext = NULL;
	return p;
}
void nhap(MHnode &l, int n)
{
	MH x[100];
	NodeMH *p;
	for (int i = 1; i <= n; i++)
	{
		cout << "Nhap mat hang thu " << i << " :" << endl;
		nhapmathang(x[i]);
		p = GetNode(x[i]);
		AddTail(l, p);
	}
}
