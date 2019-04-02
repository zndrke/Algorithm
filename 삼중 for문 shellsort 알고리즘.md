삼중 for문 shellsort 알고리즘

~~~c
#include <stdio.h>

void shellsort(int v[], int n)
{
	int gap, i, j, temp;

	for (gap = n / 2;gap > 0; gap /= 2)		
		for (i = gap;i < n;i++)
			for (j = i - gap;j >= 0 && v[j] > v[j + gap];j -= gap) {
				temp = v[j];
				v[j] = v[j + gap];
				v[j + gap] = temp;		
				//if v[j]<v[j+gap] then replace
			}
}


int main(void) {
	int s[] = { 12,73,4,51,22,71,2,68,100,35 };
	int i;
	int m = sizeof(s) / sizeof(int);

	for (i = 0;i < m;i++)
		printf("%4d", s[i]);
	putchar('\n');

	shellsort(s, m);
	for (i = 0;i < m;i++)
		printf("%4d", s[i]);
	putchar('\n');

	return 0;
}
~~~



셸 정렬은 삽입 정렬을 보완한 알고리즘이다.

삽입정렬에서 요소간 거리가 멀 경우 많은 이동을 하게된다.

삽입정렬이 어느정도 정렬된 배열에 대해서 빠른것을 착안하였고, gap을 사용하여 정렬한다.



gap은  초기는 에는  gap=n/2 각 회전할 때 마다 gap을 반으로 나눈다.



먼 요소간의 정렬을 어느정도 하고 마지막에 gap을 1로 하여 전체에 대해 삽입정렬을 하면

삽입정렬의 단점을 보완한 shellsort가 된다.