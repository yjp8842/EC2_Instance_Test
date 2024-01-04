### EC2_Instance_Test

<hr>
<br>

T계열 인스턴스 성능 측정

- small
  - t2.small
  - t3.small
  - t3a.small
  - t4.small

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

- t2.small = 3.025712490081787 seconds
- t3.small = 2.4270567893981934 seconds
- t3a.small = 2.573723316192627 seconds
- t4g.small = 1.0078325271606445 seconds
