seletion, insertion, bubble 비교



1. selection_sort

~~~c
#include <stdio.h>
#define SWAP(x, y, t) ( (t)=(x), (x)=(y), (y)=(t) )

void selection_sort(int list[], int n)
{	int i, j, least, temp;
	for(i=0; i<n-1; i++) {
		least = i;
		for(j=i+1; j<n; j++) 			// 최솟값 탐색
			if(list[j]<list[least]) least = j;
		SWAP(list[i], list[least], temp);
	}
}

int main(void){
	int list[]= {2,3,8,5,4,1};
	int i;
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
		printf("\n");
	selection_sort(list,6);
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
	
}
~~~

선택 정렬

시간 복잡도 = O(n^2)

비교 횟수 = n(n-1)/2

이동 횟수 = 3(n-1)

메모리 효율이 좋음





2. insertion_sort

~~~c
#include <stdio.h>

// 삽입정렬
void insertion_sort(int list[], int n)       	
{   
   int i, j, key;
   for(i=1; i<n; i++){
   	key = list[i];
	for(j=i-1; j>=0 && list[j]>key; j--) 
		list[j+1] = list[j]; 		// 레코드의 오른쪽 이동
    	list[j+1] = key;
   }
}


int main(void){
	int list[]= {2,3,8,5,4,1};
	int i;
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
		printf("\n");
	insertion_sort(list,6);
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
	
}
~~~

삽입 정렬

시간복잡도 

최선의 경우 (이미 정렬된 경우)= O(n)

최악의 경우 (역순으로 정렬된 경우) = O(n^2)

평균의 경우 = O(n^2)

많은 이동이 필요하므로 레코드가 클 경우 불리함

대부분 정렬되어 있으면 매우 효율적 => shell_sort 착안



3. bubble_sort

~~~c
#include <stdio.h>
#define SWAP(x, y, t) ( (t)=(x), (x)=(y), (y)=(t) )

void bubble_sort(int list[], int n)
{  
   int i, j, temp;
   for(i=n-1; i>0; i--){
		for(j=0; j<i; j++) 	// 앞뒤의 레코드를 비교한 후 교체
	      if(list[j]>list[j+1])   
     		    SWAP(list[j], list[j+1], temp);
   }
}


int main(void){
	int list[]= {2,3,8,5,4,1};
	int i;
	for(i=0;i<sizeof(list)/sizeof(int);i++)
		printf("%d ",list[i]);
		printf("\n");
	bubble_sort(list,6);
	for(i=0;i<6;i++)
		printf("%d ",list[i]);
	
}
~~~

버블 정렬

비교 횟수는 최선, 최악, 평균 모두 O(n^2)

이동 횟수

최악의 경우(역순)= 이동횟수 *3

최선의 경우(이미 정렬된 경우)= 0

평균 = O(n^2)



레코드의 이동 연산이 과다하여 삽입정렬의 하위버전으로 여겨짐