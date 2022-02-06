# 7.0 Introduction



&#x20;Here are the steps of our algorithm:

1. Start by pushing the `root` node to the queue.
2. Keep iterating until the queue is empty.
3. In each iteration, first count the elements in the queue (let’s call it `levelSize`). We will have these many nodes in the current level.
4. Next, remove `levelSize` nodes from the queue and push their `value` in an array to represent the current level.
5. After removing each node from the queue, insert both of its children into the queue.
6. If the queue is not empty, repeat from step 3 for the next level.

Example 1:

![](<../.gitbook/assets/image (9).png>)

![](<../.gitbook/assets/image (8).png>)



![](<../.gitbook/assets/image (11).png>)

![](<../.gitbook/assets/image (10) (1).png>)

![](<../.gitbook/assets/image (5).png>)

![](<../.gitbook/assets/image (7).png>)

![](<../.gitbook/assets/image (12).png>)

![](<../.gitbook/assets/image (13).png>)
