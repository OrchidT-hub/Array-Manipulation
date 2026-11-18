# Array-Manipulation
A C program for array insertion, deletion, display, sorting, and searching.
## STudent Information
Name:Tasmim Jannat
ID:26002159
Course:BSC in CSE
## Experiment Title
Array Manipulation
## Objective
•	To learn how to insert and delete elements in an array.
•	To understand and implement Bubble Sort, Insertion Sort, and Selection Sort.
•	To learn Linear Search and Binary Search.
•	To count the number of comparisons in both searching methods.
•	To understand how different sorting and searching algorithms work.
## Problem Analysis
In this experiment, we are given an array of distinct integers. We need to insert a new value at a given position and delete an existing value from the array. After updating the array, we need to sort it using three different sorting methods: Bubble Sort, Insertion Sort, and Selection Sort. We also need to search for a specific value using Linear Search on the unsorted array and Binary Search on the sorted array. Finally, we have to show whether the value is found and count the number of comparisons made during searching.
## Solution Approach
First, we take the array size and elements as input from the user. Then, we insert a new value at the given position by shifting the elements to the right. After that, we delete the given value by shifting the remaining elements to the left.
Next, we make three copies of the updated array and sort them using Bubble Sort, Insertion Sort, and Selection Sort. Finally, we perform Linear Search on the updated unsorted array and Binary Search on the sorted array. We also count the comparisons made during both searches.
## Algorithm
Step 1: Start.
Step 2: Take the array size and elements as input.
Step 3: Take the insertion position and new value.
Step 4: Insert the new value at the given position by shifting the elements to the right.
Step 5: Take the value to be deleted and remove it from the array.
Step 6: Take the search target.
Step 7: Make three copies of the updated array.
Step 8: Apply Bubble Sort, Insertion Sort and Selection Sort to the three copies.
Step 9: Perform Linear Search on the updated unsorted array.
Step 10: Perform Binary Search on the sorted array.
Step 11: Count and display the comparisons made during both searches.
Step 12: Display all results.
Step 13: Stop.

## Implementation
code

#include<stdio.h>
void bubbleSort(int arr[],int n)
{
    int i,j,temp;
    for(i=0; i<n-1; i++)
    {
        for(j=0; j<n-i-1; j++)
        {
            if(arr[j] > arr[j + 1])
            {
                temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
    }
}
void insertionSort(int arr[],int n)
{
    int i,j,key;

    for(i=1; i<n; i++)
    {
        key=arr[i];
        j=i-1;
        while(j>=0 && arr[j]>key)
        {
            arr[j+1]=arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
void selectionSort(int arr[],int n)
{
    int i,j,min,temp;

    for(i=0; i<n-1; i++)
    {
        min=i;
        for(j=i+1; j<n; j++)
        {
            if(arr[j]<arr[min])
            {
                min=j;
            }
        }
        temp=arr[i];
        arr[i]=arr[min];
        arr[min]=temp;
    }
}
int linearSearch(int arr[],int n,int target,int *count)
{
    int i;
    *count = 0;
    for(i=0; i<n; i++)
    {
        (*count)++;

        if(arr[i]==target)
        {
            return i;
        }
    }
    return -1;
}
int binarySearch(int arr[],int n,int target,int *count)
{
    int low=0, high=n-1,mid;
    *count=0;
    while(low<=high)
    {
        mid=low+((high-low)/2);
        (*count)++;

        if(arr[mid] == target)
        {
            return mid;
        }
        else if(target<arr[mid])
        {
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }
    return -1;
}
void display(int arr[],int n)
{
    int i;
    for(i=0; i<n; i++)
    {
        printf("%d ",arr[i]);
    }
    printf("\n");
}
int main()
{
    int n,i,arr[100],bubble[100],insertion[100],selection[100];
    int pos,X,del,target;
    int linearResult,binaryResult,linearCount,binaryCount;

    scanf("%d", &n);
    for(i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    scanf("%d %d", &pos, &X);

    for(i=n; i>pos; i--)
    {
        arr[i]=arr[i-1];
    }
    arr[pos]=X;
    n++;

    scanf("%d",&del);

    for(i=0; i<n; i++)
    {
        if(arr[i]==del)
        {
            break;
        }
    }
    for(i=i; i<n-1; i++)
    {
        arr[i]=arr[i + 1];
    }
    n--;

    scanf("%d", &target);

    //Display
    printf("Updated Array: ");
    display(arr, n);


    for(i = 0; i < n; i++)
    {
        bubble[i]=arr[i];
        insertion[i]=arr[i];
        selection[i]=arr[i];
    }

    bubbleSort(bubble, n);
    insertionSort(insertion, n);
    selectionSort(selection, n);

    printf("Bubble Sort: ");
    display(bubble, n);
    printf("Insertion Sort: ");
    display(insertion, n);
    printf("Selection Sort: ");
    display(selection, n);

    linearResult=linearSearch(arr, n, target, &linearCount);
    if(linearResult != -1)
    {
        printf("Linear Search: Found at Index %d (Comparisons: %d)\n",linearResult,linearCount);
    }
    else
    {
        printf("Linear Search: Not Found (Comparisons: %d)\n",linearCount);
    }


    binaryResult=binarySearch(bubble, n, target, &binaryCount);
    if(binaryResult!= -1)
    {
        printf("Binary Search: Found at Index %d (Comparisons: %d)\n",binaryResult, binaryCount);
    }
    else
    {
        printf("Binary Search: Not Found (Comparisons: %d)\n",binaryCount);
    }
    
    return 0;
}
## Result
Case#1Input:
7
42 15 33 8 27 19 50
3 24
33
42
Case#1Output:
Updated Array: 42 15 24 8 27 19 50
Bubble Sort: 8 15 19 24 27 42 50
Insertion Sort: 8 15 19 24 27 42 50
Selection Sort: 8 15 19 24 27 42 50
Linear Search: Found at Index 0 (Comparisons: 1)
Binary Search: Found at Index 5 (Comparisons: 2)
Case#2Input:
6
30 25 20 15 10 5
2 12
25
18
Case#2Output:
Updated Array: 30 12 20 15 10 5
Bubble Sort: 5 10 12 15 20 30
Insertion Sort: 5 10 12 15 20 30
Selection Sort: 5 10 12 15 20 30
Linear Search: Not Found (Comparisons: 6)
Binary Search: Not Found (Comparisons: 3)
The program was successfully executed and tested with the given sample inputs. It correctly inserted and deleted values from the array and displayed the updated array. All three sorting algorithms (bubble, insertion and selection) sorted the elements correctly and both searching methods (linear and binary) showed the correct results with the number of comparisons.
## Complexity Analysis
Insertion and deletion may take more time when the array becomes larger. The three sorting algorithms may need many comparisons. Linear Search checks elements one by one, while Binary Search needs fewer comparisons because it searches in a sorted array by dividing the search area into half.
## Discussion
In this experiment, we learned how to insert and delete elements from an array and how different sorting and searching algorithms work. We noticed that all three sorting algorithms produced the same sorted output but they use different methods to arrange the elements. Linear Search checks each element one by one while Binary Search is faster because it works on a sorted array by dividing the search area into half each time. We also learned how to count the number of comparisons during searching.

## Conclusion
From this experiment, we learned how to perform basic array operations using C programming. We also understood the working process of Sorting (Bubble Sort, Insertion Sort and Selection Sort) and Searching (Linear Search and Binary Search). This experiment helped us understand the differences between these algorithms and their time complexities.
