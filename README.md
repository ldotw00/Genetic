## 유전알고리즘을 통한 회귀식 작성하기



우리에게 주어진 데이터는 225 ~ 235레벨 구간에서의 1재획당 먹는 경험치 비율이다.<br>
<br>
이와 관련된 설명은 [재획비란.md](https://github.com/ldotw5121/Genetic/blob/master/재획비란.md)파일에 작성되어있으며<br>
<br>
데이터에 관해서는 [225-235레벨 구간에서 1재획당 먹는 경험치 비율.md](https://github.com/ldotw5121/Genetic/blob/master/225-235%EB%A0%88%EB%B2%A8%20%EA%B5%AC%EA%B0%84%EC%97%90%EC%84%9C%201%EC%9E%AC%ED%9A%8D%EB%8B%B9%20%EB%A8%B9%EB%8A%94%20%EA%B2%BD%ED%97%98%EC%B9%98%20%EB%B9%84%EC%9C%A8.md) 파일에 작성되어있다.<br>
<br>
이 데이터를 이용하여 회귀식을 작성해보자.<br>
선형회귀를 한다는 가정을 전제로 할 것이며 이에 따라서 식은 y= ax+b의 형태로 나타난다.<br>
<br>
<br>
<br>
여기서 우리가 유전 알고리즘으로 구해야 할 것은 기울기인 a의 값과 절편인 b의 값<br>
초기 데이터로 구한 기울기와 유전 알고리즘을 거쳐 나온 데이터로 구한 기울기 값과 절편 값을 각각 합하고, 각각의 평균을 통해서 a와 b의 최종값을 결정할 수 있을 것이다.<br>
<br>
다음은 초기 데이터의 점 그래프이다.<br>
<br>
![datapoint](https://user-images.githubusercontent.com/62733730/85315037-4c669580-b4f5-11ea-8934-5a355dfe5004.jpg)
<br>
일단 초기 데이터로 본다면 a의 값은 X_0(225,32.83) 과 X_10(235,13.01) 이 선택되므로 <br>
(13.01-32.83)/(235-225) = -1.982이다.<br>
y=-1.982x +b이므로<br>
한 점 X0를 대입하면 b = 478.78<br>
따라서 초기데이터에서의 식은 y = -1.982x+478.78 이다.<br>
<br>
![](https://user-images.githubusercontent.com/62733730/85315058-57212a80-b4f5-11ea-86e0-7fdfb63a0909.jpg)
<br>
자 이제 유전 알고리즘을 이용해보겠다.<br>
<br>
일단 두 점을 찾으면 되기 때문에 후보해를 두 가지로 설정해도 되겠지만, 만약 그 후보해가 돌연변이 과정에서 값을 이탈할 경우도 있기 때문에 안전하게 네 가지 후보해를 설정해보도록 하겠다. <br>
<br>
네 가지 후보해는 랜덤으로 선택한다.<br>
<br>
이번에는 228, 225, 230, 232가 선택되었다고 가정하겠다.<br>
<br>
각각에 해당하는 경험치 비율은 29.11, 32.83, 15.31, 13.95이다.<br>
이 경험치 비율의 합은 88.2이므로<br>
룰렛 원반의 면적은 ((각각의 값/88.2)*100)로 32%, 36%, 17%, 15% 에 해당한다.<br>
<br>
룰렛을 돌려서 후보해 4개를 뽑아낸다.<br>
15% 1번 36%1번 32% 2번이 나왔다고 가정하겠다.<br>
<br>
그렇다면 15%와 32%를 묶고, 32%와 36%를 묶어서 교차를 진행한다.<br>
<br>
<br>
<br>
첫번째 묶음에 대한 교차연산과 돌연변이 연산을 수행하는 과정이다.<br>
<br>
15%에 해당하는 x값은 232, 32%에 해당하는 x값은 228이므로<br>
232의 이진변환 11101000<br>
228의 이진변환 11100100<br>
<br>
5/3으로 쪼개서 교차하면<br>
11101110 (238)<br>
11100000 (224)<br>
<br>
돌연변이 연산으로는 값의 편차치를 생각해서 6번째의 수가 0이면 1로 1이면 0으로 치환한다.<br>
<br>
11101010(234)<br>
11100100(228)<br>
<br>
<br>
<br>
두번째 묶음에 대한 교차연산과 돌연변이 연산을 수행하는 과정이다.<br>
<br>
32%에 해당하는 x값은 228 36%에 해당하는 x값은 225이므로<br>
228의 이진변환 11100100<br>
225의 이진변환 11100001<br>
<br><br>
5/3으로 쪼개서 교차하면<br>
11100001(225)<br>
11100100(228)<br>
<br>
마찬가지로 값의 편차치를 생각하여, 6번째의 수가 0이면 1로 1이면 0으로 치환한다.<br>
11100101(229)<br>
11100000(224)<br>
<br>

<br>
여기까지의 계산과정에서 가장 큰 수와 가장 작은 수로 계산을 해보면<br>
가장 큰 수는 234이고 가장 작은 수는 224이다.<br>
<br>
다만 224는 고려사항이 아니므로 제외하면, 228이라 볼 수 있겠다.<br>
<br>
<br>
<br>
x가 234인 점은 그래프에서 X_9(234,13.51)이고 x가 228인 점은 X_3(228,29.11)이므로<br>
이 두 점을 통해 기울기 a1을 구하게 되면<br>
(13.51-29.11)/(234-228) = -2.6이다.<br>
그리고 y1 = -2.6x1+b1에 X_3을 대입하면 b1 = 621.91로<br>
<br>
유전 알고리즘을 한 번 거친 식은 y1 = -2.6x1+621.91이다.<br>


![genoneline](https://user-images.githubusercontent.com/62733730/85315074-5be5de80-b4f5-11ea-8515-470a3048096b.jpg)
<br>
이후로도 여러번 유전알고리즘을 통해서 식이 많이 나올 것이다.<br>
<br>
그리고 식이 많을수록 더 정확한 값을 구할 수 있을 것이다.<br>
다만 여기서는 가독성을 위해서 한 번의 유전 알고리즘만 거치고 계산을 해보겠다.<br>
<br>
<br>
<br>
초기데이터의 식과 유전알고리즘을 한 번 거쳐 나온 식을 통해 회귀식을 작성해보면<br>
<br>
기울기의 값은 a+a1의 평균값, 절편값은 b+b1의 평균값<br>
<br>
따라서 회귀식은<br>
<br>
Y = (-1.982 -2.6 /2)X + (478.78 + 621.91/2)<br>
<br>
Y = -2.291X + 550.345이다.<br>

![genoneplusfirstline](https://user-images.githubusercontent.com/62733730/85315098-63a58300-b4f5-11ea-858e-6b784e6a97cd.jpg)

