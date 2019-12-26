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
拿图一举例。车站用点来表示，道路用边来表示。一条边上的数字代表从其一端的车站到另一端所花的时间。顶点S内的数字代表S的车辆数。给出的每个车站的最大容量为10。为了解决S3的问题，我们有两条不同的最短路。<br>
+ 1.PBMC->S1->S3，在这种情况下，PBMC需要带4辆自行车，因为我们可以从S1获得一辆多余的自行车，然后带5辆车去S3,这样两个车站都是最佳状态。
+ 2.PBMC->S2->S3,这条路所花时间与S1一样，但是只需要带3辆自行车，所以最后会选择这条路。
---

+ *代码实现*
```java
import java.util.ArrayList;
import java.util.Scanner;
 
public class Main {
    private static int Cmax;
    private static int N;
    private static int Sp;
    private static int M;
    private static ArrayList<Integer> path = new ArrayList<Integer>();      //暂存当前路径，退层的时候移除退层的那个点
    public static ArrayList<Integer> result;                              //暂存已经得到的一条最短路径
    private static int minTime = Integer.MAX_VALUE;                         //暂存路径的行使时间
    private static int send;
    private static int collect;
    private static boolean[] visited;
    private static int []C;
    /**
     *
     * @param from          前一个结点，用于在后面定位路径
     * @param cur           当前深入的结点
     * @param des           目的地，也就是目标结点
     * @param adj           图的邻接矩阵
     * @param time          当前寻找这条路径的累计时间
     */
    public static void dfs(int from, int cur, int des, int [][]adj,int time){       //time是当前这条路径目前累计的行走时间
        visited[cur] = true;
        path.add(cur);
        time += adj[from][cur];
        if(cur == des){
            /**
             * 遍历在ArrayList中存的这条路径
             * 计算当前这条路的路程长度
             * 计算需要从老家带出来几辆自行车
             * 计算需要带回老家几辆自行车
             */
            int s = 0, c = 0;
            for(int i = 1 ;i < path.size(); i++){        //注意要跳过起点开始
                int j = path.get(i);
                if(C[j] > Cmax / 2 ){
                    c += (C[j] - Cmax / 2);
                }
                else if(C[j] < Cmax / 2){
                    if(c > (Cmax / 2) - C[j]){
                        c -= (Cmax / 2 - C[j]);
                    }
                    else{
                        s += ((Cmax / 2) - C[j] - c);
                        c = 0;
                    }
                }
            }
            if(time == minTime){
                if(s < send || (s == send && c < collect)){
                    minTime = time;
                    result = new ArrayList<Integer>(path);
                    send = s;
                    collect = c;
                }
            }
            else if(time < minTime){
                minTime = time;
                result = new ArrayList<Integer>(path);
                send = s;
                collect = c;
            }
        }
        else{       //深度遍历
            for(int i = 0;i < N;i++){
                if(!visited[i] && adj[cur][i] != 0){
                    dfs(cur, i, des, adj, time);
                }
            }
        }
        //退层操作
        path.remove(path.size() - 1);
        visited[cur] = false;
    }
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Cmax = in.nextInt();    //每个站点最大容量
        N = in.nextInt();   //总站点数
        N = N + 1;
        Sp = in.nextInt();  //问题站点的下标
        M = in.nextInt();   //路的条数
        C = new int[N];
        int [][]adj = new int[N][N];
        visited = new boolean[N];
        for(int i = 1;i < N;i++){
            C[i] = in.nextInt();
        }
        int Si, Sj, Tij;
        for(int i = 0 ;i < M; i++){
            Si = in.nextInt();
            Sj = in.nextInt();
            Tij = in.nextInt();
            adj[Si][Sj] = Tij;
            adj[Sj][Si] = Tij;
        }
        dfs(0, 0, Sp, adj, 0);
        System.out.print(send+" ");
        for(int i = 0;i<result.size()-1;i++)
        System.out.print(result.get(i)+"->");
        System.out.print(result.get(result.size()-1)+" ");
        System.out.println(collect);
    }
}
```
