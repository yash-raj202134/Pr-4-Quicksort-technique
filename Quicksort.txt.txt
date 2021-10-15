// A program to perform Quick sort using recursion and iteration concepts..
#include <iostream>
using namespace std;

class QuickSort
{
    int piviot, partition_index;
    // Data members
public:
    int Asize;
    int Arr[];
    void printArray(int *A) // A function to print Array content
    {
        for (int i = 0; i < Asize; i++)
            cout << A[i] << " ";
        cout << endl;
    }
    void getArray(int *A, int n) // A function to get array elements
    {
        cout << "Enter the unsorted array : ";
        for (int i = 0; i < n; i++)
            cin >> A[i];
        Asize = n;
    }
    void swap(int &a, int &b) // swap function
    {
        int temp;
        temp = a;
        a = b;
        b = temp;
    }
    int partition(int *, int, int);
    void quickSortRecursive(int *, int, int);
    void quickSortIterative(int *, int);
};
typedef QuickSort qs;
int qs ::partition(int *A, int low, int high) // Partition function
{
    piviot = A[low];
    int i, j;
    i = low + 1;
    j = high;
    do
    {
        while (A[i] <= piviot)
            i++;
        while (A[j] > piviot)
            j--;
        if (i < j)
            swap(A[i], A[j]);
    } while (i < j);
    swap(A[low], A[j]);
    return j;
}
void qs::quickSortRecursive(int *A, int low, int high) // Quick sort function for recursion concept
{
    if (low < high)
    {
        partition_index = partition(A, low, high);
        quickSortRecursive(A, low, partition_index - 1);
        quickSortRecursive(A, partition_index + 1, high);
    }
}

void qs::quickSortIterative(int *A, int n) // Quick sort function for iterative process
{
    int stack[n];
    int top = -1;
    int lo = 0, hi = n - 1;
    stack[++top] = lo;
    stack[++top] = hi;
    while (top >= 0)
    {
        hi = stack[top--];
        lo = stack[top--];
        int p = partition(A, lo, hi);
        if (p - 1 > lo)
        {
            stack[++top] = lo;
            stack[++top] = p - 1;
        }
        if (p + 1 < hi)
        {
            stack[++top] = p + 1;
            stack[++top] = hi;
        }
    }
}

int main(void)
{
    qs q;
    q.getArray(q.Arr, 5);
    cout << "Before sorting : ";
    q.printArray(q.Arr);
    q.quickSortRecursive(q.Arr, 0, 4);
    cout << "After sorting : ";
    q.printArray(q.Arr);

    cout << "\n BY ITERATION \n";
    qs s;
    s.getArray(s.Arr, 8);
    cout << "Before sorting : ";
    s.printArray(s.Arr);
    s.quickSortIterative(s.Arr, 8);
    cout << "After sorting : ";
    s.printArray(s.Arr);

    return 0;
}