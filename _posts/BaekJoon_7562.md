---
layout: post
title:  "백준 7562번 - 나이트의 이동"
date:   2024-09-04
categories: blog
layout: post
---

## 문제

---

<img src="/assets/img/screenshot/7562.png">

---

## 풀이

---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
	static int[][] able = {
		{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
		{2, -1}, {2, 1}, {1, -2}, {1, 2}
	};

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int testCaseCount = Integer.parseInt(br.readLine());

		for(int i = 0; i < testCaseCount; i++) {
			int N = Integer.parseInt(br.readLine());

			boolean[][] isVisited = new boolean[N][N];

			String[] knightPosStr = br.readLine().split(" ");
			String[] targetPosStr = br.readLine().split(" ");

			int[] knightPos = {
				Integer.parseInt(knightPosStr[0]),
				Integer.parseInt(knightPosStr[1])
			};

			int[] targetPos = {
				Integer.parseInt(targetPosStr[0]),
				Integer.parseInt(targetPosStr[1])
			};

			System.out.println(bfs(knightPos, targetPos, isVisited));
		}
	}

	public static int bfs(int[] knightPos, int[] targetPos, boolean[][] isVisited) {
		if(knightPos[0] == targetPos[0] && knightPos[1] == targetPos[1]) {
			return 0;
		}
		
		Queue<int[]> queue = new LinkedList<>();
		queue.add(new int[]{knightPos[0], knightPos[1], 0});
		isVisited[knightPos[0]][knightPos[1]] = true;
		int length = isVisited.length;

		while(!queue.isEmpty()) {
			int[] current = queue.poll();
			int r = current[0];
			int c = current[1];
			int count = current[2];

			for (int[] move : able) {
				if (r == targetPos[0] && c == targetPos[1]) {
					return count;
				}

				int dr = r + move[0];
				int dc = c + move[1];

				if (validate(dr, dc, length, isVisited)) {
					isVisited[dr][dc] = true;
					queue.add(new int[]{dr, dc, count + 1});
				}
			}
		}
		return -1;
	}

	public static boolean validate(int dr, int dc, int length, boolean[][] isVisited) {
		return dr >= 0 && dc >= 0 && dr < length && dc < length && !isVisited[dr][dc];
	}
}

```