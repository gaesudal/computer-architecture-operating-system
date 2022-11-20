## 2.1 0과 1로 숫자를 표현하는 방법

0과 1을 나타내는 가장 작은 정보 단위를 **비트** 라고함

| 1바이트 | 8비트 |
| --- | --- |
| 1킬로바이트 | 1000바이트 |
| 1메가바이트 | 1000킬로바이트 |
| 1기가바이트 | 1000메가바이트 |
| 1테라바이트 | 1000기가바이트 |

0과 1만으로 모든 숫자를 표현하는 방법을 **이진법** 이라고 함

이진수의 음수 표현 : 모든 이진수의 0과 1을 뒤집은 수를 **1의 보수** 거기에 1을 더한 값을 **2의 보수** 라고 함

실제로 이진수만 봐서는 음수인지 양수인지 구분하기 어렵기 때문에 컴퓨터 내부에서 어떤 수를 다룰 때는 이 수가 양수인지 음수인지를 구분하기 위해 **플래그**를 사용

한글자로 열여섯 종류 (0~9, A~F)의 정보를 표현하면 **십육진수**

## 2.2 0과 1로 문자를 표현하는 방법

컴퓨터가 인식하고 표현할 수 있는 문자의 모음을 **문자 집합(character set)** 이라 함

문자를 0과 1로 변환해야 비로소 컴퓨터가 이해 할 수 있음, 이 변환 과정을 **문자 인코딩** 이라고 하고 인코딩 후 0과 1로 이루어진 결과값이 문자 코드가 됨

인코딩의 반대 과정, 즉 0과 1로 이루어진 문자 코드를 사람이 이해할 수 있는 문자로 변환하는 과정은 **문자 디코딩** 이라고 함

- 아스키코드 : 초창기 문자 집합 중 하나로, 2^7개로 총 128개의 문자를  표현 할 수 있음.
    
    1비트를 추가한 8비트의 확장 아스키가 등장하기도 했지만, 256개도 부족했기 때문에, 이런 이유로 등장한 한글 인코딩 방식이 **EUC-KR**
    
- EUC-KR : 한글 인코딩 방식에는 완성형 (한글 완성형 인코딩)과 조합형 (한글 조합형 인코딩)이 존재
    - 완성형 인코딩 : 초성, 중성, 종성의 조합으로 이루어진 완성된 하나의 글자에 고유한 코드를 부여
    - 조합형 인코딩 : 초성을 위한 비트열, 중성을 위한 비트열, 종성을 위한 비트열을 할당하여 그것들의 조합으로 하나의 글자 코드를 완성하는 인코딩 방식
    
    EUC-KR은 대표적인 완성형 인코딩 방식. 초성, 중성, 종성이 모두결합된 한글 단어에 2바이트 크기의 코드를 부여. EUC-KR의 확장된 버전으로 **CP949** 가 있음
    

언어별로 인코딩하는 수고로움을 해결하기 위하여 등장한 것이 **유니코드** 문자 집합

가장 대중적으로 쓰이는 것은 **UTF-8**