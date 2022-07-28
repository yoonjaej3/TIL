## JAVA 출력

- 1차원 배열 : toString
- 다차원 배열 : deepToString

```
import java.util.Arrays;

public class ArrayExec {
	public static void main(String[] args) {

		int[] arr = {5,2,1,6,7};

		System.out.println(Arrays.toString(arr));
	}
}

 [5, 2, 1, 6, 7]
```

```
import java.util.Arrays;

public class ArrayExe {
	public static void main(String[] args) {

		int[][] arr = {{1,2,3,4,5},{5,4,3,2,1}};

		System.out.println(Arrays.deepToString(arr));
	}
}
[[1, 2, 3, 4, 5], [5, 4, 3, 2, 1]] 
```
