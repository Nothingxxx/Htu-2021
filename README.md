# Htu-2021
henanshifandaxue
#include<iostream>
#include<stdio.h>
#include<stdlib.h>
using namespace std;
template<class Type>
///例如：5 25 55   10 20 30
//@1--将数组a先一分为2
//@2--将数组两两进行判断并在数组a比较之后的最小元素放进d数组中
//@3--当两组比较完后，进行条件判断
//@4--当剩下的是左边时，则说明是右边的开始界限已经超出了范围，则进行循环将剩下的数组直接copy到d数组
//@5--当剩下的是右边时，则说明是左边的开始界限已经超出了范围，则进行循环将剩下的数组直接copy到d数组
void Merger(Type a[], Type d[], int left, int mid, int right)///将有序的两个数组进行合并（也叫合并排序）
{
    int i = left, j = mid + 1, k = left;
    while ((i <= mid) && (j <= right))///要保证当两边的界限在一定范围内才能比较
    {
        if (a[i] <= a[j])
            d[k++] = a[i++];
        else
            d[k++] = a[j++];
    }
    if (i > mid)///当左边的界限超出范围时，则说明剩下最右边的数组；
    {
        for (int p = j; p <= right; p++)
            d[k++] = a[p];
    }
    else
    {
        for (int p = i; p <= mid; p++)
            d[k++] = a[p];
    }
}
template<class Type>
void MergerSort(Type a[], int left, int right)
{
    int*d=new int[right];
    if (left < right)///至少有两个点
    {
        int i = (left + right) / 2;
        MergerSort(a, left, i);//分治法(分而治之)不断的分左边
        MergerSort(a, i + 1, right);///在分右边
        //当两边只剩下一个数的时候
        Merger(a, d, left, i, right);
        for (int p = left; p <= right; p++)
            a[p] = d[p];///复制回数组a(因为最后我要输出a数组)
    }
}
int main()
{
    int a[] = {1,3,5,7,9,2,4,6,8,10 };
    int b[10];
    MergerSort(a, 0, 8);
    for (int i = 0; i < 10; i++)
        cout << a[i] << "  ";
    return 0;
}
