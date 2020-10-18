---
layout: archive
permalink: /algorithms/linked_lists/single_merge
title: "Linked Lists- Merge two Sorted Singulary Linked Lists"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/Linked_Lists/single_merge/Page1.jpg)
![inserting an Image](/images/Linked_Lists/single_merge/Page2.jpg)
![inserting an Image](/images/Linked_Lists/single_merge/Page3.jpg)
![inserting an Image](/images/Linked_Lists/single_merge/Page4.jpg)
![inserting an Image](/images/Linked_Lists/single_merge/Page5.jpg)


Code:

    def merge_sorted(self, llist):
        
        p = self.head
        q = llist.head
        s = None
        
        if not p:
            return q
        
        if not q:
            return p
        
        if p and q:
            if p.data <= q.data:
                s = p
                p = s.next
            else:
                s = q
                q = s.next
            
            new_head = s
                    
        while p and q:
            
            if p.data <= q.data:
                s.next = p
                s = p
                p = s.next
            
            else:
                s.next = q
                s = q
                q = s.next
        
        if not p:
            s.next = q
        
        if not q:
            s.next = p
        
        return new_head



