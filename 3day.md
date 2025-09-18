문제 해결 포트폴리오
이 문서는 색종이 문제를 해결하며 겪었던 시행착오와 그 과정에서 얻은 학습 내용을 기록합니다. 문제를 분석하고, 오류를 찾아내며, 더 효율적인 코드를 작성하는 과정을 통해 프로그래밍 실력이 어떻게 성장했는지 보여주는 것이 목표입니다.

색종이 문제 해결 과정
1. 문제 설명
주어진 색종이의 위치와 크기를 바탕으로, 여러 장의 색종이가 겹쳐졌을 때 전체 면적을 계산하는 파이썬 코드입니다.

2. 초기 접근과 시행착오
문제를 처음 해결할 때, input()을 어떻게 처리해야 하는지, 그리고 map() 함수를 어떻게 사용해야 하는지에 대해 어려움을 겪었습니다. 두 개의 숫자를 한 줄에 입력받는 예제에 맞춰 코드를 작성하는 것이 힘들었고, while문을 사용해 올바른 입력이 들어올 때까지 반복하는 논리를 만드는 것도 쉽지 않았습니다.

Python

# 초기 코드
# 두 개의 input()을 사용해 각 숫자를 따로 입력받으려 시도함
num_of_papers = int(input())

if num_of_papers <= 100:
    covered_area = set()
    for i in range(num_of_papers):
        while True:
            try:
                a = int(input())
                if 1 <= a <= 100:
                    break
                else:
                    print("다시,입력하세요")
            except ValueError:
                print("숫자를 입력해주세요")
        
        while True:
            try:
                b = int(input())
                if 1 <= b <= 100:
                    break
                else:
                    print("다시,입력하세요")
            except ValueError:
                print("숫자를 입력해주세요")

        for x in range(a, a + 10):
            for y in range(b, b + 10):
                covered_area.add((x, y))
    
    print(len(covered_area))

else:
    print("100이하로 다시입력")
3. 리팩토링과 개선된 코드
초기 코드의 복잡성을 줄이고 재사용성을 높이기 위해 함수화(Refactoring)를 진행했습니다. def를 이용해 코드를 함수로 묶고, return을 사용해 결과값을 반환하도록 수정했습니다.

Python

# 최종 리팩토링된 코드
# 함수를 호출하기 전에 색종이 개수를 받습니다.
num_of_papers = int(input())

def colorpaper_area(num_of_papers):
    if num_of_papers <= 100:
        covered_area = set()
        for i in range(num_of_papers):
            while True:
                try:
                    a, b = map(int, input().split())
                    if (1 <= a <= 100) and (1 <= b <= 100):
                        break
                    else:
                        print("1에서 100 사이의 두 자연수를 입력해주세요.")
                except ValueError:
                    print("숫자를 입력해주세요.")
            
            for x in range(a, a + 10):
                for y in range(b, b + 10):
                    covered_area.add((x, y))
        return len(covered_area)
    else:
        print("100이하로 다시입력")

# 함수를 호출하고 결과를 출력합니다.
result = colorpaper_area(num_of_papers)
print(result)
4. 겪었던 오류와 해결 과정
들여쓰기 오류와 return 문제
def 함수와 if, for 문 사이의 관계를 명확히 하는 데 어려움을 겪어 IndentationError가 계속 발생했습니다. 눈에 보이지 않는 **탭(Tab)**과 **스페이스(Space)**의 차이가 오류의 원인이었으며, return을 for문 안에 잘못 배치해 함수가 한 번만 실행되는 논리적 오류도 있었습니다. 결국 모든 들여쓰기를 지우고 스페이스바 4번으로 처음부터 다시 작성하는 방법으로 해결했습니다.

ValueError (터미널 경로 오류)
들여쓰기 오류를 해결한 후, 코드를 실행했을 때 ValueError가 발생했습니다. 이 오류는 코드가 아니라, 코드를 실행하는 터미널 환경 때문에 발생한다는 것을 알게 되었습니다. input() 함수는 사용자로부터 직접 값을 입력받는 역할을 하지만, 터미널이 파일 경로를 사용자의 입력으로 착각하면서 오류가 발생했던 것입니다. python 파일이름.py와 같이 간단한 명령어로 코드를 실행한 뒤, 터미널이 입력을 기다릴 때 숫자만 입력함으로써 이 문제를 해결했습니다.

5. 학습 내용
이 프로젝트를 통해 다음과 같은 역량을 키울 수 있었습니다.

문제 분석: input()과 map()의 차이를 이해하고 문제의 요구사항을 정확히 분석하는 법을 배웠습니다.

디버깅: 코드가 완벽하더라도, 실행하는 환경에 따라 다른 오류가 발생할 수 있다는 것을 배웠습니다.

리팩토링의 중요성: return을 사용해 함수를 만드니 코드가 더 깨끗해지고 재활용하기 쉬워졌습니다.

오류 해결: IndentationError나 ValueError와 같이 낯선 오류 메시지를 스스로 분석하고 해결하는 능력을 키웠습니다.