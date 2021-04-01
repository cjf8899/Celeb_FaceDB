# Custom FaceDB
## Demo

Coming soon~


## 1. Crawling

* 코드 및 Visual Studio Code, Python 다운로드
  * 크롤러 코드 다운로드 링크 : [WebCrawler_exe](https://github.com/cjf8899/WebCrawler_exe)
* 현재 chrome 버전 정보를 확인, 버전에 맞는 chromedriver를 다운로드
  * 자신의 크롬 버전을 찾고 chromedriver 다운로드
  * 크롬버젼 확인 링크 : chrome://settings/help  
  * chromedriver 다운로드 링크 : [chromedriver](https://chromedriver.chromium.org/downloads)
<p align="left"><img src="./Crawling_demo.gif" width="70%" height="70%" title="70px" alt="memoryblock"></p>


## 2. FaceDB Menual
* 크롤링한 이미지를 front, side, back 폴더를 만든 후 사진을 구별하여 분류

<p align="left"><img src="https://user-images.githubusercontent.com/53032349/113259936-a6a84880-9308-11eb-8988-e15e0b398c46.JPG" width="45%" height="45%" title="70px" alt="memoryblock">　　<img src="https://user-images.githubusercontent.com/53032349/113259986-b889eb80-9308-11eb-8bf2-bddf5c284df2.png" width="45%" height="45%" title="70px" alt="memoryblock"></p><br>

* 분류 후 이름을 코드로 재설정(코드는 따로 공개 X)<br>
* 검색어 인물 이외의 다른 사람이 존재해도 무방
  * 다른 인물은 **Etc** 로 분류
  
<p align="left"><img src="https://user-images.githubusercontent.com/53032349/113262205-52eb2e80-930b-11eb-8730-ffe6e80c3291.JPG" width="70%" height="70%" title="70px" alt="memoryblock"></p>

### 2.1 Images Example
* Front
 <p align="left"><img src="https://user-images.githubusercontent.com/53032349/113263317-92664a80-930c-11eb-9c72-c0f133173aac.JPG" width="70%" height="70%" title="70px" alt="memoryblock"></p><br>
 
* Side
 <p align="left"><img src="https://user-images.githubusercontent.com/53032349/113263469-c6da0680-930c-11eb-9ce3-79afa3b251c2.JPG" width="70%" height="70%" title="70px" alt="memoryblock"></p><br>
 
* Back
 <p align="left"><img src="https://user-images.githubusercontent.com/53032349/113263555-e3763e80-930c-11eb-8aa2-bd2b9b35402d.JPG" width="70%" height="70%" title="70px" alt="memoryblock"></p>

## 3. Category Classification tool
* category tool은 이미지를 front, side, back, delete로 쉽게 분류
<p align="left"><img src="https://user-images.githubusercontent.com/53032349/113265991-b37c6a80-930f-11eb-8a5a-91413df9b757.JPG" width="40%" height="40%" title="70px" alt="memoryblock">　　<img src="https://user-images.githubusercontent.com/53032349/113266035-bbd4a580-930f-11eb-89de-b78f9971018e.JPG" width="30%" height="30%" title="70px" alt="memoryblock"></p><br>

* 자세한 설명 링크 : [Classify_imgFile_tool](https://github.com/xylitol/Dataset_tools/tree/main/classify_imgFile_tool)
