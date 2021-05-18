# 작업 스케줄링(Job Scheduling)

##### n개의 작업, 각 작업의 수행 시간, 그리고 m개의 동일한 기계가 주어질 때 모든 작업이 가장 빨리 종료되도록 작업을 기계에 배정하는 문제 (단, 한 작업은 배정된 기계에서 연속적으로 수행되어야 한다. 또한 기계는 한 번에 하나의 작업만을 수행한다.)

- 최적 해 : brute force 알고리즘 이용
- 근사 해: greedy 알고리즘 이용 (현재까지 배정된 작업에 대해서 가장 빨리 끝나는 기계에 새 작업 배정)

------

## 코드

- 입력 : n개의 작업 개수, 각 작업 수행 시간, 기계 개수
- 출력 : 모든 작업이 종료된 시간

```java
while (TaskList != 0) {
            int i;
            for (i = 0; i <= MachineSize; i++) {			// 작업 중에서 가장 이른 시작시간 task[1]을 가져온다
                if (machine[i][task[1].start] == 0) {		// task[1]을 수행할 기계가 있으면 그 기계에 task[1]을 배정
                    for (int j = task[1].start; j < task[1].end; j++)
                        machine[i][j] = t;
                    break;
                }
            }
            if (machine[i][task[1].start] == 0) {			
                MachineSize++;
                for (int j = task[1].start; j < task[1].end; j++)
                    machine[MachineSize][j] = t;
            }
            delete(task);
            t++;											// 모든 작업들이 기계에 배정 될 때까지 반복
        }
```



## 시간 복잡도

##### Greedy 알고리즘

n개의 작업을 하나씩 가장 빨리 끝나는 기계에 배정, for 루프 m - 1번 수행

모든 기계의 마지막 작업 종료 시간을 살펴보기 : O(m)

= > ***n x O(m) + O(m) = O(nm)***



## 근사 비율

##### 근사해를 OPT'라 하고 최적해를 OPT라고 할 때,  OPT' ≤ 2 x OPT

###### (근사해는 최적해의 2배를 넘지 않는다)

------

**WHY?**

가장 마지막으로 배정된 작업 i가 T부터 수행되며 모든 작업이 T + ti에 종료됨 (OPT' = T + ti)

<img width="382" alt="작업1" src="https://user-images.githubusercontent.com/80511341/118688798-572ec500-b841-11eb-8c1e-28be34ad8719.PNG">

T'는 작업 i를 제외한 모든 작업의 수행 시간의 합을 기계의 수 m으로 나눈 값( = 작업 i를 제외한 평균 종료 시간)

**T <= T'** (가장 늦게 끝나는 기계를 제외한 모든 기계에 배정된 작업은 적어도 T 이후에 종료되기 때문)

-  T <= T' 를 이용한 OPT' ≤ 2 x OPT 증명

<img width="535" alt="작업2" src="https://user-images.githubusercontent.com/80511341/118688820-5b5ae280-b841-11eb-88f5-c9d736ee17a1.PNG">

------

n = [2, 3, 4, 5] (작업의 개수)

m = 2 (기계의 개수)



