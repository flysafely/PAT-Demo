There is a public bike service in Hangzhou City which provides great convenience to the tourists from all over the world. 
One may rent a bike at any station and return it to any other stations in the city.
The Public Bike Management Center (PBMC) keeps monitoring the real-time capacity of all the stations. 
A station is said to be in perfect condition if it is exactly half-full. 
If a station is full or empty, PBMC will collect or send bikes to adjust the condition of that station to perfect. 
And more, all the stations on the way will be adjusted as well.
When a problem station is reported, PBMC will always choose the shortest path to reach that station. 
If there are more than one shortest path, the one that requires the least number of bikes sent from PBMC will be chosen.
---
翻译:<br>
杭州的公共自行车为来自世界各地的游客提供了巨大的方便。
游客可以在任意一个车站借自行车并在其他任意一个车站归还。
公共自行车管理中心（PBMC）一直在监视各个车站的实时容量。
当一个车站的车辆正好等于最大容量的一半时，就称为最佳状态。
如果一个车站的车辆数是满的或是空的，则PBMC将会回收或送去一些自行车来使该车站到达最佳状态。
还有，所有沿路的车站也会被调配到最佳状态。

![Figure 1](https://github.com/flysafely/PAT-Demo/blob/master/Figures/Public%20Bike%20Managemen.jpg)

+ Figure 1 illustrates an example. 
  The stations are represented by vertices and the roads correspond to the edges. 
  The number on an edge is the time taken to reach one end station from another. 
  The number written inside a vertex S is the current number of bikes stored at S. Given that the maximum capacity of each station is 10. 
  To solve the problem at S3 , we have 2 different shortest paths:
  + 1. PBMC -> S1 -> S3 . In this case, 4 bikes must be sent from PBMC, because we can collect 1 bike from S1 and then take 5 bikes to S3 , so that both stations will be in perfect conditions.
  + 2. PBMC -> S2 -> S3 . This path requires the same time as path 1, but only 3 bikes sent from PBMC and hence is the one that will be chosen.
---
翻译:<br>
当一个问题车站被上报了，PBMC总是会选择到达该车站的最短路。如果有多条最短路，则选择PBMC需要送的最少的路线。
拿图一举例。车站用点来表示，道路用边来表示。一条边上的数字代表从其一端的车站到另一端所花的时间。顶点S内的数字代表S的车辆数。给出的每个车站的最大容量为10。为了解决S3的问题，我们有两条不同的最短路。
1.PBMC->S1->S3，在这种情况下，PBMC需要带4辆自行车，因为我们可以从S1获得一辆多余的自行车，然后带5辆车去S3,这样两个车站都是最佳状态。
2.PBMC->S2->S3,这条路所花时间与S1一样，但是只需要带3辆自行车，所以最后会选择这条路。
