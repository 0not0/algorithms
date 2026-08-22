# [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/description/)  

<code>Medium</code> level  

You are given a network of <code>n</code> nodes, labeled from <code>1</code> to <code>n</code>. You are also given <code>times</code>, a list of travel times as directed edges <code>times[i] = (u<sub>i</sub>, v<sub>i</sub>, w<sub>i</sub>)</code>, where <code>u<sub>i</sub></code> is the source node, <code>v<sub>i</sub></code> is the target node, and <code>w<sub>i</sub></code> is the time it takes for a signal to travel from source to target.  
We will send a signal from a given node <code>k</code>. Return <i>the <strong>minimum</strong> time it takes for all the <code>n</code> nodes to receive the signal</i>. If it is impossible for all the n nodes to receive the signal, return <code>-1</code>.  

<strong>Example 1:</strong>   

<img alt="" src="../../images/dikstra/743/743-network-delay-time.png" style="height: 220px; width: 200px;" />  

<pre>
<strong>Input:</strong> times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
<strong>Output:</strong> 2
</pre>  

<strong>Example 2:</strong>  

<pre>
<strong>Input:</strong> times = [[1,2,1]], n = 2, k = 1
<strong>Output:</strong> 1
</pre>  

<strong>Example 3:</strong> 

<pre>
<strong>Input:</strong> times = [[1,2,1]], n = 2, k = 2
<strong>Output:</strong> -1
</pre>  

<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 <= k <= n <= 100</code></li>
	<li><code>1 <= times.length <= 6000</code></li>
	<li><code>times[i].length == 3</code></li>
	<li><code>1 <= u<sub>i</sub>, v<sub>i</sub> <= n</code></li>
	<li><code>u<sub>i</sub> != v<sub>i</sub></code></li>
	<li><code>0 <= w<sub>i</sub> <= 100</code></li>
	<li>All the pairs <code>(u<sub>i</sub>, v<sub>i</sub>)</code> are <strong>unique</strong>. (i.e., no multiple edges.)</li>
</ul>  
<br/>

***

<h3>Solution</h3>

Оскільки потрібно швидко обходити сусідів вершини, використовуємо <strong>[список суміжності](https://github.com/smykhailevskyi/algorithms/blob/main/data%20structures/graph/graph_representations.md)</strong>.  
Використовуємо <strong>priority_queue (min-heap)</strong>, щоб кожного разу брати вершину з найменшим поточним часом.  
Виконуємо <strong>релаксацію ребер (Edge Relaxation)</strong> 

<strong>Time complexity:</strong> <code>O((V + E) log V)</code>, <em>priority_queue</em> робить <em>push/pop</em> за час <code>log V</code>.  
<strong>Space complexity:</strong> <code>O(V + E)</code>  
де:  
<code>V (Vertices)</code> - кількість вершин  
<code>E (Edges)</code> - кількість ребер.  

Реалізація на <strong>C++</strong>

```C++
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<vector<pair<int,int>>> graph(n + 1);

        for (auto &edge : times) {
            graph[edge[0]].push_back({edge[1], edge[2]});
        }

        vector<int> dist(n + 1, INT_MAX);
        dist[k] = 0;

        priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;

        pq.push({0, k});

        while (!pq.empty()) {
            auto [time, node] = pq.top();
            pq.pop();

            if (time > dist[node])
                continue;

            for (auto &[next, weight] : graph[node]) {
                if (dist[next] > dist[node] + weight) {
                    dist[next] = dist[node] + weight;
                    pq.push({dist[next], next});
                }
            }
        }

        int answer = 0;

        for (int i = 1; i <= n; i++) {
            if (dist[i] == INT_MAX)
                return -1;

            answer = max(answer, dist[i]);
        }

        return answer;
    }
};
```

