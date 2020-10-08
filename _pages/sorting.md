---
layout: archive
permalink: /algorithms/sorting
title: "Sorting Algorithms"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

heres where sorting algorithms will go:

Merge Sort Algorithm:


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