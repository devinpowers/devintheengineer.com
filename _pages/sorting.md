---
layout: archive
permalink: /algorithms/sorting
title: "Sorting Algorithms"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

heres where sorting algorithms will go:

## Insertion Sort 

    from time import time
    ''' insertion sort Algorithm'''


    def insertion_sort(list_to_sort):
        
        indexing_length = range(1, len(list_to_sort))
            
        for i in indexing_length:
            
            value_to_sort = list_to_sort[i]
            
            
            while list_to_sort[i-1] > value_to_sort and i>0: # python allows negative indexing
                
                list_to_sort[i], list_to_sort[i-1] = list_to_sort[i-1], list_to_sort[i]
            
                i = i -1  # move down the sorted list to check if number is less than the previous number
            
        return list_to_sort


    array = [7,2,1,6,8,5,3,102,1,31,45,232,4,25,12,8,2,4,2,0,9,12,6,2,4,1,3]

    start_time = time()

    sorted_array = insertion_sort(array)

    end_time = time()

    print('Time to Complete Soring:', end_time-start_time)
    print(sorted_array)

## Merge Sort

    import time
    '''Merge Sort Function Built By ME!!!!!'''

    def Merge(Left, Right, Array):
        
        Left_length = len(Left)
            
        Right_length = len(Right)
        
        i = j = k = 0
            
        while (i < Left_length and j < Right_length):
            
            if Left[i] <= Right[j]:
                Array[k] = Left[i]
                i = i + 1
            
            else:
                Array[k] = Right[j]  
                j = j+ 1
            k = k + 1
            
        # in case one of the letters runs out before the other
        while i < Left_length:
            
            Array[k] = Left[i]
            i = i + 1
            k = k + 1
            
        while j < Right_length:
            
            Array[k] = Right[j]
            j = j + 1
            k = k + 1
            
        return Array

    def Merge_Sort(Array): 
        '''Recursive function to sort an Array'''
        n = len(Array)
        
        if n < 2:    
            return
        middle = n // 2
        
            # have to make right and left subarrays        
        Left = Array[0:middle]
            
        Right = Array[middle:]
    
            #Recursive functions

        Merge_Sort(Left)
        
        Merge_Sort(Right)
        
        # calling the merge function
        Merge(Left, Right, Array)

    b = [6,90,1,8,54,67,0,23,900,67,6,8,12,6]
    a = [2,4,1,6,8,5,3,7]

    start= time.time()

    Merge_Sort(a) 
    print(a)

    End = time.time()

    #print('Time to solve algo:', End - start)
    Merge_Sort(b)

## Quick Sort

    from time import time

    '''QuickSort!!!!!!'''

    def Partition(A ,start, end):
        
        pivot = A[end]
    
        p_index = start
        
        
        for i in range(start,end):
            
            if A[i] <= pivot:
                
                #swap number at index with the P_index!
                A[p_index], A[i] = A[i], A[p_index]
                
                p_index = p_index +1
                
        # this is swaping the pivot point between the sorted values
        
        A[p_index], A[end] = A[end], A[p_index]

        
        return p_index
        
            
    def QuickSort(A, start, end):
        
        if start > end:
            return
        
        p_index = Partition(A, start, end)
        
        # recursive Calls here:
            
        QuickSort(A, start, p_index-1)
        
        QuickSort(A,p_index +1, end)
        
        

    array = [7,2,1,6,8,5,3,102,1,31,45,232,4,25,12,8,2,4,2,0,9,12,6,2,4,1,3,2,0,12121,8,349,169,420,55,83,4,6,7,8,4,42,32,100,12,23,4,32,5,6,546,43,2,69,70,69]

    n = len(array)

    start_time = time()

    QuickSort(array,0,n-1)

    end_time = time()

    print('Time to Complete Soring:', end_time-start_time)

    print(array)


