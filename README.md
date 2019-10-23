// Name: Jeffrey Bindeman
// ProbID: 469

import java.io.*;
import java.util.*;

public class Main {

	public static Scanner in = new Scanner(System.in);
	public static int[] dy = new int[]{1, 1, 0, -1, -1, -1, 0, 1};
	public static int[] dx = new int[]{0, -1, -1, -1, 0, 1, 1, 1};

	public static void main(String[] args) {

		int cases = in.nextInt();
		String s, str;
		ArrayList<String> arrStorage = new ArrayList<>();
		for (int i = 0; i < cases; i++) {

			for (int j = 0; j < 99; j++) {
				if (in.hasNextInt()) {
					break;
				}
				arrStorage.add(in.next());
			}

			int r = arrStorage.size() + 2;
			int c = arrStorage.get(0).length() + 2;

			char[][] worldMap = new char[r][c];

			for (int j = 0; j < r; j++) {
				if (j == 0 || j == r - 1) {
					for (int k = 0; k < c; k++) {
						worldMap[j][k] = 'L';
					}
				}
				else {
					worldMap[j] = ("L" + arrStorage.get(j - 1) + "L").toCharArray();
				}
			}
			arrStorage.clear();
//
//			for (int j = 0; j < r; j++) {
//				for (int k = 0; k < c; k++) {
//					System.out.print(worldMap[j][k]);
//				}
//				System.out.println("");
//			}
//			System.out.println("");

			int debug = 1;
			while (in.hasNext()) {

				s = in.next();
				if (s.charAt(0) == 'W' || s.charAt(0) == 'L') {
					arrStorage.add(s);
					break;
				}

				int y = Integer.parseInt(s), x = in.nextInt();
				int lakeSize = findLakeSize(worldMap, y, x);
				returnLake(worldMap, y, x);

//				System.out.println("Case " + (i + 1) + "." + debug);
				System.out.println(lakeSize);
				debug++;
			}

			if (in.hasNext()) {
				System.out.println("");
			}
		}

	}

	public static int findLakeSize(char[][] map, int y, int x) {
		char temp = map[y][x];
		map[y][x] = '.';
		int count = 1;

		for (int i = 0; i < dy.length; i++) {
			if (map[y + dy[i]][x + dx[i]] == temp) {
				count += findLakeSize(map, y + dy[i], x + dx[i]);
			}
		}

		return count;

	}

	public static void returnLake(char[][] map, int y, int x) {
		char temp = map[y][x];
		map[y][x] = 'W';

		for (int i = 0; i < dy.length; i++) {
			if (map[y + dy[i]][x + dx[i]] == temp) {
				returnLake(map, y + dy[i], x + dx[i]);
			}
		}

	}

}
