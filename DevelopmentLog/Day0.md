### 210912 항해 0일차
목표: 시작하기 전에 깃 사용법 숙지, 리포지토리 정리, 백준 python3 입력 어떻게 받는지 알아보기

#### 1.깃 사용법 숙지
1) 깃허브 리포지토리 만들기
2) git clone 하기
3) 아무파일 하나 올리기(주로 README.md)
echo "# Playground" >> README.md  
git init  
git add README.md  
git commit -m "first commit"  
git branch -M main  
git remote add origin (해당 리포지토리 주소)  
git push -u origin main  


#### 2.리포지토리 정리
git subtree add --prefix=(해당 Repository 하위의 디렉터리 구조) (옮겨올 Repository 주소) (옮겨올 Repository의 branch)  
를 이용하면 리포지토리가 옮겨진다.  
subtree는 이동이 아니라 복사되기 때문에 기존 리포지토리는 삭제했다.  
리포지토리 만들고 setting에서 manage에서 협업 신청 보내기  

#### 3.백준 python3 입력 어떻게 받는지 알아보기
```python
# sys.stdin.readline() 이용
import sys
a, b = map(int, sys.stdin.readline().split())
print(a+b)

# input() 이용
a, b = map(int, input().split())
print(a+b) 
```
https://jjluveeecom.tistory.com/30 여기서 참조했다. 첫번째가 더 빠르다고 한다. 왜 그런지는 나중에 더 찾아보자

#### 일기
내일 드디어 항해 시작이다! 설레고 기대 되지만 여러가지 걱정이 앞선다.  
이 때까지 배웠던 것들을 잘 활용해서 재밌는 프로젝트를 만들었으면 좋겠다!!😎  
99일동안 일기가 잘 이어지길 바란다...ㅋㅋㅋ 앞으로 분량이 줄어들 수 있지만(아마 필연적일 것이다) 조금이라도 배운 내용을 적을 수 있으면 좋겠다.