---
layout: archive
permalink: /algorithms/linked_lists/rotate
title: "Linked Lists- Rotate around Pivot"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/Linked_Lists/rotate/Page1.jpg)
![inserting an Image](/images/Linked_Lists/rotate/Page2.jpg)
![inserting an Image](/images/Linked_Lists/rotate/Page3.jpg)


Code: Method 1:

        def rotate(self, k):

                p = self.head
                q = self.head

                previous = None
                count = 0

                while p and count < k:

                    previous  = p

                    p = p.next
                    q = q.next

                    count += 1

                p = previous

                while q:

                    previous = q
                    q = q.next

                q = previous

                print(q.data)

Code: Method 2:

        def rotate(self, data):

            cur = self.head

            while cur.next:

                if cur.data == data:
                    pivot = cur
                cur = cur.next

            cur.next = self.head
            self.head = pivot.next
            pivot.next = None


