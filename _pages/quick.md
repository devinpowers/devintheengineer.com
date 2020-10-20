---
layout: archive
permalink: /algorithms/quick
title: "Post-Order Tree Traversal"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/sorting/merge/Page1.jpg)
![inserting an Image](/images/sorting/merge/Page2.jpg)
![inserting an Image](/images/sorting/merge/Page3.jpg)
![inserting an Image](/images/sorting/merge/Page4.jpg)
![inserting an Image](/images/sorting/merge/Page5.jpg)
![inserting an Image](/images/sorting/merge/Page6.jpg)
![inserting an Image](/images/sorting/merge/Page7.jpg)
![inserting an Image](/images/sorting/merge/Page8.jpg)
![inserting an Image](/images/sorting/merge/Page9.jpg)
![inserting an Image](/images/sorting/merge/Page10.jpg)
![inserting an Image](/images/sorting/merge/Page11.jpg)
![inserting an Image](/images/sorting/merge/Page12.jpg)


Code:

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


