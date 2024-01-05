### EC2_Instance_Test

<hr>

### T계열 인스턴스 성능 측정

- small
  - t2.small
  - t3.small
  - t3a.small
  - t4.small

<br>

#### 테스트 코드

```python
from flask import Flask
import requests
from bs4 import BeautifulSoup
import time

app = Flask(__name__)

@app.route('/')
def hello_world():
    # 제공된 Github URL 목록
    urls = [
        "https://jinhyeonkwak.github.io/JinhyeonKwak/",
        "https://kkh0331.github.io/kkh0331/",
        "https://lrozlo.github.io/Lrozlo/",
        "https://eastwon0103.github.io/EastWon0103/",
        "https://allllfo.github.io/allllfo/",
        "https://bkkmw.github.io/bkkmw/",
        "https://lvolzdev.github.io/lvolzdev/",
        "https://kimyoungseok15.github.io/kimyoungseok15/",
        "https://rlafl7942.github.io/rlafl7942/",
        "https://youhyeoneee.github.io/youhyeoneee/",
        "https://jkl0124.github.io/jkl0124/",
        "https://seohee99.github.io/seohee99/",
        "https://ye-s-rin.github.io/ye-s-rin/",
        "https://yjp8842.github.io/yjp8842/",
        "https://euics.github.io/euics/",
        "https://jiminpark23.github.io/jiminpark23/",
        "https://parkjineon.github.io/parkjineon/",
        "https://baebyeolha.github.io/baebyeolha/",
        "https://seo-yj.github.io/SEO-YJ/",
        "https://tomk2d.github.io/Tomk2d/",
        "https://eunxoo.github.io/eunxoo/",
        "https://sjjuunny.github.io/SJJuunnY/",
        "https://yeongseoyoo.github.io/YeongseoYoo/",
        "https://gundolflee.github.io/gundolflee/",
        "https://sjun516.github.io/sjun516/",
        "https://godltjsdud.github.io/godltjsdud/",
        "https://seungtoctoc.github.io/seungtoctoc/",
        "https://eehanseul.github.io/eehanseul/",
        "https://hleeat.github.io/hleeat/",
        "https://github.com/NOEL-code/WOO_SUNG/",
        "https://chanjin1998.github.io/chanjin1998/",
        "https://chaeheonjeong.github.io/chaeheonjeong/",
        "https://heeeesoo.github.io/heeeesoo/",
        "https://ekgus9701.github.io/ekgus9701/",
        "https://beomseok37.github.io/beomseok37/",
        "https://bookeers.github.io/bookeers/"
    ]

    results = []
    total_time = 0  # 전체 통신 시간을 계산하기 위한 변수
    start_time = time.time()  # 요청 시작 시간
    for url in urls:
        response = requests.get(url)
        if response.status_code == 200:
            html = response.text
            soup = BeautifulSoup(html, 'html.parser')
            content = soup.select('body > div')
            content_str = ''.join(map(str, content))
            results.append(f"\n\n\n" + content_str)
        else:
            results.append(f"URL: {url} - Error: " + str(response.status_code))

    end_time = time.time()  # 요청 종료 시간
    total_time += end_time - start_time

    # 모든 요청의 총 시간을 결과에 추가
    results.append(f"Total Time: {total_time} seconds")

    # 결과들을 HTML 개행으로 구분하여 반환
    return '<br><br>'.join(results)

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

<br>

### 테스트 결과

|인스턴스 유형|시간 측정 결과|
|------|---|
|t2.small|3.025712490081787 seconds|
|t3.small|2.4270567893981934 seconds|
|t3a.small|2.573723316192627 seconds|
|t4g.small|1.0078325271606445 seconds|

<br>

### 결과 정리

1. 왜 T계열 small 인스턴스들을 비교하려 했는지?
	- 처음에 만든 인스턴스가 t4g.small이어서 이 계열의 인스턴스들을 비교해보고 싶었음.

2. T계열 인스턴스들 간의 차이가 어떻게 나는지?
	- t4g.small > t3.small > t3a.small > t2.small

3. 그렇게 차이가 나는 이유에 대해 어떻게 생각하는지?
	- 일단 t 옆에 붙어있는 숫자가 세대라고 하는데, 세대가 올라갈수록 더 성능이 
		좋아지지 않을까라고 처음에 생각함.
	- t2는 네트워크 성능이 낮음에서 중간이었음.
	- t3 시리즈: Intel Skylake 프로세서
	- t4 시리즈: AWS Graviton2 프로세서
		- Intel Skylake 프로세서는 데스크탑 및 서버 시장을 대상으로 하는 x86-64 아키텍처 기반의 프로세서
		- AWS Graviton2는 Amazon의 클라우드 컴퓨팅 서비스인 EC2에서 사용되는 64코어 Arm 기반 서버 칩

#### 소감
- EC2 인스턴스를 처음 만들어보았고, 단어들도 너무 생소해서 실습하는데 어려움이 조금 많았다. 몇 번 지우고 생성하다보니 보다 익숙해졌지만, 성능들을 비교하라고 하니 또 어려움이 많았다.
하지만 인스턴스 성능을 자세히 조사해볼 수 있는 기회가 되어서 나름 유익하고 좋았던 것 같다.
	