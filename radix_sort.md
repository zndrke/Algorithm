radix_sort

~~~c
#include <stdio.h>
#include <stdlib.h>

#define MAX_QUEUE_SIZE 100
typedef int element;
typedef struct { // 큐 타입
	element  data[MAX_QUEUE_SIZE];
	int  front, rear;
} QueueType;

// 오류 함수
void error(char *message)
{
	fprintf(stderr, "%s\n", message);
	exit(1);
}

// 공백 상태 검출 함수
void init_queue(QueueType *q)
{
	q->front = q->rear = 0;
}

// 공백 상태 검출 함수
int is_empty(QueueType *q)
{
	return (q->front == q->rear);
}

// 포화 상태 검출 함수
int is_full(QueueType *q)
{
	return ((q->rear + 1) % MAX_QUEUE_SIZE == q->front);
}

// 삽입 함수
void enqueue(QueueType *q, element item)
{
	if (is_full(q))
		error("큐가 포화상태입니다");
	q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;
	q->data[q->rear] = item;
}

// 삭제 함수
element dequeue(QueueType *q)
{
	if (is_empty(q))
		error("큐가 공백상태입니다");
	q->front = (q->front + 1) % MAX_QUEUE_SIZE;
	return q->data[q->front];
}

#define BUCKETS 10	//10진수이므로 10개
#define DIGITS  4	//최대 자릿수
void radix_sort(int list[], int n)
{
	int i, b, d, factor = 1;
	QueueType queues[BUCKETS];	//10개의 큐를 생성

	for (b = 0; b<BUCKETS; b++) init_queue(&queues[b]);  // 큐들의 초기화

	for (d = 0; d<DIGITS; d++) {
		for (i = 0; i<n; i++)			// 데이터들을 자리수에 따라 큐에 삽입
			enqueue(&queues[(list[i] / factor) % 10], list[i]);

		for (b = i = 0; b<BUCKETS; b++)  // 버킷에서 꺼내어 list로 합친다.
			while (!is_empty(&queues[b]))
				list[i++] = dequeue(&queues[b]);
		factor *= 10;					// 그 다음 자리수로 간다.
	}
}

#define  SIZE 10	

int main(void)
{
	int list[SIZE];
	srand(time(NULL));
	int i;
	for (i = 0; i<SIZE; i++)      	// 난수 생성 및 출력 
		list[i] = rand() % 100;		//1부터 100까지 10개 숫자

	radix_sort(list, SIZE); // 기수정렬 호출 
	for (i = 0; i<SIZE; i++)
		printf("%d ", list[i]);
	printf("\n");
	return 0;
}
~~~

기수 정렬

기수정렬은 O(dn)의 선형의 시간 복잡도를 가진다. 

d는 자리수, n은 데이터의 개수, bucket은 해당 키의 표현과 밀접하다. 

예를 들어 10진수의 경우 10개의 bucket, 2진수의 경우 2개, 알파벳의 경우 26개의 bucket을 사용

기수정렬은 d가 작을 수록 효과적인 알고리즘 이다. 

만약 d가 n만큼 커질 경우 O(n^2)이 되어 단순 정렬 알고리즘과 비슷한 시간복잡도를 갖게 된다.