
# 진자운동 데이터 처리

아두이노에서 측정한 진자운동 데이터를 pandas 라이브러리를 통해 xlsx 파일로 내보내며, matplotlib 라이브러리를 통해 실시간 미리보기를 보여줍니다.

> **확인된 사항에 의하면, 윈도우 계열에서는 그래프가 켜져있는 상황에서 파이썬이 심각할정도로 느려짐이 확인되었습니다. Windows 계열에서는 `DISABLE_GRAPH=False` 를 `DISABLE_GRAPH=True` 로 바꿔주세요**

> **Windows 계열 OS 에서는 aioconsole 이 호환되지 않는것으로 나타났습니다. Windows 계열에서는 `DISABLE_AIOCONSOLE=False` 를 `DISABLE_AIOCONSOLE=True` 로 바꿔주세요**

## 결과물

|||
|-|-|
| ![graph](./images/graph.png) | ![xlsx](./images/xlsx.png) |

## 사용과정

[python.org](https://www.python.org) 에서 파이썬을 다운받습니다.

이 저장소 페이지 상단에 초록 Code 버튼을 누르고 Donwload ZIP 를 눌러 파일을 받습니다.

받은 zip 파일을 풀고 풀린 폴더에 들어가서 cmd 창을 엽니다 (탐색기 주소 부분을 클릭하고 cmd 입력후 엔터)

```
pip install -r requirement.txt
```

필요한 파이썬 모듈을 받습니다.

그 후 main.py 파일을 적절히 수정합니다

포트 부분에 아두이노 창에서
도구 => 포트 부분에 따옴포 안에 적힌걸 옮겨 적으면 됩니다 (괄호 부분은 적지말고)

SERIAL_PORT="/dev/ttyACM0"
BAUDRATE=9600

보드레이트는 아두이노에서 설정한대로 적어주면 됩니다 (Serial.begin(9600) 이면 9600, 대부분 건들일 필요 없음)

> Windows 계열 OS (Windows 10, Windows 11 등) 에서는 `DISABLE_GRAPH=False` 를 `DISABLE_GRAPH=True` 로
> `DISABLE_AIOCONSOLE=False` 를 `DISABLE_AIOCONSOLE=True` 로 바꾸어주어야 코드가 정상작동합니다

편집된 아두이노 코드파일은 sketch_may30a 에 들어있습니다.

수정한 파이썬 파일을 저장하고, 아두이노 편집기를 완전히 끕니다 (중요! 파이썬과 아두이노 편집기가 같이 아두이노 출력을 읽으려 하면 오류가 발생합니다.)

이제 cmd 명령창에 python main.py 를 입력합니다.

측정을 완료했다면 cmd 명령창에 엔터를 입력합니다.

그러면 폴더에 끝난 시간을 이름으로 하는 엑셀 파일이 생성됩니다. 이 엑셀 파일에는 시간(second) 거리(cm) 이 담겨있습니다.

## 주의사항

열린 그래프 창을 직접 닫지 마세요, 명령창에 엔터키를 누르면 파일이 저장되며 자동으로 닫히게 됩니다.
그래프 창을 직접 닫으면 스레드 풀이 난장판이 되어(...) 파일이 저장되지 못할 수 있습니다. (리눅스 기준 그렇게 하면 세그폴트납니다)

측정 시간은 오차를 없에기 위해 아두이노의 내부시계를 이용합니다. 이 내부 시계는 최대치가 있으며 해당 값을 넘어가면 오버플로우로 음수 값이 출력될 수 있습니다.

시간이 음수가 출력되는 경우, 아두이노를 컴퓨터에서 분리한 후, 다시 연결하고 대략 10초쯤 뒤 다시 파이썬을 실행해 주세요.

엑셀파일은 이름에 시간이 적힌 채로 저장됩니다.
(e: 5월.31일.2시.53분.55초.xlsx)
template.xlsx 는 데이터가 들어가기 위한 틀에 해당하는 파일로 편집하면 안됩니다.

## 기타

확인하지 않았지만, 윈도우는 디바이스 구현이 매우 달라 표시상 딜레이가 있을 수 있습니다.
그러나 저장되는 xlsx 파일에는 아두이노 내부 시계 정보가 들어가므로 아마도 딜레이가 없어야합니다.

파일이 완전히 잘못되었다면, 유닉스 호환 시스템에서(macos, linux, bsd, ... 등의 os) 실행해야할 수 있습니다.

**확인된 사항에 의하면, 윈도우 계열에서는 그래프가 켜져있는 상황에서 파이썬이 심각할정도로 느려짐이 확인되었습니다. Windows 계열에서는 `DISABLE_GRAPH=False` 를 `DISABLE_GRAPH=True` 로 바꿔주세요**
**Windows 계열 OS 에서는 aioconsole 이 호환되지 않는것으로 나타났습니다. Windows 계열에서는 `DISABLE_AIOCONSOLE=False` 를 `DISABLE_AIOCONSOLE=True` 로 바꿔주세요**
~~얼마나 윈도우가 혐오스러운지 모르겠습니다; 느려 터지기만 하면 모르겠는데 호환성도 박살나있고 똑바로 돌아가는게 전혀 없네요.~~
