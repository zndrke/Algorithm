merge_sort

~~~c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 1000

int sorted[MAX_SIZE];   // 추가 공간이 필요

		/* i는 정렬된 왼쪽 리스트에 대한 인덱스
		j는 정렬된 오른쪽 리스트에 대한 인덱스
		k는 정렬될 리스트에 대한 인덱스 
		l은 남아있는 리스트에 대한 인덱스 */
void merge(int list[], int left, int mid, int right)
{
	int i, j, k, l; 
	i = left;  j = mid + 1;  k = left;

	/* 분할 정렬된 list의 합병 */
	while (i <= mid && j <= right) {
		if (list[i] <= list[j])
			sorted[k++] = list[i++];	//k증가 i 증가 
		else
			sorted[k++] = list[j++];	//k증가 j 증가 
	}
	if (i>mid)	/* 남아 있는 레코드의 일괄 복사 */
		for (l = j; l <= right; l++)
			sorted[k++] = list[l];
	else	/* 남아 있는 레코드의 일괄 복사 */
		for (l = i; l <= mid; l++)
			sorted[k++] = list[l];
	/* 배열 sorted[]의 리스트를 배열 list[]로 재복사 */
	for (l = left; l <= right; l++)
		list[l] = sorted[l];
}
//
void merge_sort(int list[], int left, int right)
{
	int mid;
	if (left<right) {	//요소가 하나일 때는 merge_sort하지 않고 리턴 
		mid = (left + right) / 2;     /* 리스트의 균등 분할 */
		merge_sort(list, left, mid);    /* 부분 리스트 정렬 */
		merge_sort(list, mid + 1, right); /* 부분 리스트 정렬 */
		merge(list, left, mid, right);    /* 합병 */
	}
}

int main(void){
	
	int list[]= {2,7,8,5,4,1};
	int i;
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
		printf("\n");
	merge_sort(list,0,6);
	for(i=1;i<7;i++)
		printf("%d ",sorted[i]); 
}
~~~

malloc없이 구현한 merge sort이다

합병정렬은 divide&conquar 알고리즘을 사용하고

리스트를 균등분할하여 재귀적으로 문제를 해결한다.

모든 경우에 대해 O(nlogn)의 시간복잡도를 가진다.

이동하는 시간이 매우 크기 때문에 연결리스트로 구현된 레코드를 정렬할 경우 매우 효율적이다.