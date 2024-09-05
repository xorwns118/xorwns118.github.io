---
layout: post
title:  "백준 16948번 - 데스나이트"
date:   2024-09-03
categories: blog
layout: post
---

## 문제

---

<img src="/assets/img/screenshot/16948.png">

---

## 풀이

---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
	static int[][] able = { {-2, -1}, {-2, +1}, {0, -2}, {0, +2}, {+2, -1}, {+2, +1} };

	public static void main(String[] args) throws IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(bf.readLine());
		String[] startEnd = bf.readLine().split(" ");

		int[] knightPos = {Integer.parseInt(startEnd[0]), Integer.parseInt(startEnd[1])};
		int[] targetPos = {Integer.parseInt(startEnd[2]), Integer.parseInt(startEnd[3])};

		boolean[][] isVisited = new boolean[N][N];
		System.out.println(bfs(knightPos, targetPos, N, isVisited));
	}

	public static int bfs(int[] knight, int[] target, int N, boolean[][] isVisited) {
		Queue<int[]> queue = new LinkedList<>();
		queue.add(new int[] {knight[0], knight[1], 0});
		isVisited[knight[0]][knight[1]] = true;

		while (!queue.isEmpty()) {
			int[] pos = queue.poll();
			int r = pos[0];
			int c = pos[1];
			int count = pos[2];

			if (r == target[0] && c == target[1]) {
				return count;
			}

			for (int[] move : able) {
				int nx = r + move[0];
				int ny = c + move[1];

				if (isValid(nx, ny, N) && !isVisited[nx][ny]) {
					isVisited[nx][ny] = true;
					queue.add(new int[] {nx, ny, count + 1});
				}
			}
		}

		return -1;
	}

	public static boolean isValid(int x, int y, int N) {
		return x >= 0 && x < N && y >= 0 && y < N;
	}
}
```