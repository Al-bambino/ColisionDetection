# Collision detection

## Here is problem description

## Solution
  * Find visible intervals of both polygons.
  * For each point on left polygon, find where it would hit right polygon.
  * Calculate distance between those two points.
  * Do the same thing for right polygon.
  * Keep track of minimum distance between those points => it's solution ;)
  
This will take **`O((n + m) * (log n + log m)).`**
  
### Find visible intervals of polygon
Visible intervals are polygon's lines (or parts of the lines) on which collision could happen.
We will use sweep line algorithm for finding them. Status structure will be `AVL tree`, so this will take **`O(n*(log n))`** time.
 - Sort points by `Y coordinate`.
 - In `sweep line status` keep track of all polygon lines that sweep line intersects.
 - Events are polygon points.  
 - For each point, get the rightmost (leftmost) line from sweep line status and update that it is visible from previously checked point to current point.
 - Add all lines that starts from that point into status structure, and delete all lines that ends in that point.
 
 ### Finding hit spot on polygon
Once we have all polygon's `visible intervals`, it's easy to find where collision could happen. 
For each point `p` on left (right) polygon, do **binary search** on visible intervals on right (left) polygon to find which interval contains p. That interval is part of (or is whole) polygon line, let's call it  `l` - collision will happen on it.
 > Notice that array with visible intervals is already sorted because we were sweeping throughout sorted points. 

Now, we now **Y coordinate** of collision - it's `p.Y`, also we know line on which collision would happen - it's `l`. We only need to find **X coordinate**. Do some math and it's here: 

> x = (y - n) / k

Doing this for `n` points we got **`O(n*(log n))`** time.
 
