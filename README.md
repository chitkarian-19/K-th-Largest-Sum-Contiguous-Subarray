# K-th-Largest-Sum-Contiguous-Subarray
You are given an array Arr of size N. You have to find the K-th largest sum of contiguous subarray within the array elements.

The question is asking for all the sums that are going to be produced, what is the kth max value that will be achieved.
The idea is quite simple to generate the sums of all subcontiguous array and store it in the list.
Once the list is achieved, sort that list in desceding order and finally return the kth max.

Here for time and space optimisation we are using a min heap rather than a list, this min heap will have a size of k.

If we use min heap then TC: 0(n^2logk)
                        SC: O(k)
                        
If we use sorting with a list TC: 0(n^2logn)
                              SC: 0(n)


Here is the approach that I am going to share for the reference

```````
class Solution {
    static PriorityQueue<Integer> pq;
    public static int kthLargest(int n, int k, int[] arr) {
        // code here
        
       pq = new PriorityQueue<Integer>();
       
       int[] pre_arr = new int[n+1];
       
       pre_arr[0]=0;
       pre_arr[1]=arr[0];
       
       for(int i=2;i<=n;i++){
         pre_arr[i]=pre_arr[i-1]+arr[i-1];
       }
       
       for(int i=0;i<n;i++){
           
           for(int j=i;j<n;j++){
               int value = pre_arr[j]-pre_arr[i]+arr[j];
               if(pq.size()<k){
                   pq.add(value);
               }
               else if(value>pq.peek())
               {
                   pq.poll();
                   pq.add(value);
               }
           }
           
       }
       
       return pq.poll();
       
        
    }
}
        



``````
