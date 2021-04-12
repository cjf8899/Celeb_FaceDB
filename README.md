# Create Celeb FaceDB
## Demo

Coming soon~


## 1. Images Crawling

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

## 4. Data Labeling 
* 라벨은 PascalVOC 포멧에 따라 xml로 제작하였고, 필요에 따라 json파일로도 변환이 가능하다.
 * xml -> json 링크 : [xml2json](https://github.com/knadh/xmlutils.py)
### 4.1 Pretreatment
* 전처리 작업으로 RatinaFace를 이용하여 이미지에서 얼굴영역을 찾은 다음, xml에 위치정보를 저장한다.
 * RetinaFece 코드 링크 : [Pytorch_retinaface](https://github.com/biubug6/Pytorch_Retinaface)

### 4.2 Work
* 전처리 과정으로 대부분의 얼굴영역은 잡혔지만, 잡히지 않은 영역은 tool을 이용하여 작업하였다.
 * tool 링크 : [labelImg](https://github.com/tzutalin/labelImg)

* 얼굴 영역을 드래그하여 선택하고 라벨을 입력한다. 라벨이 잘 못된 영역은 더블 클릭하여 수정한다.

<p align="left"><img src="https://user-images.githubusercontent.com/53032349/114352339-b9433d00-9ba6-11eb-9cc7-52fc4206ff34.JPG" width="70%" height="70%" title="70px" alt="memoryblock"></p>

### 4.3 Example
<p align="left"><img src="https://user-images.githubusercontent.com/53032349/114357537-cf53fc00-9bac-11eb-812e-97158828be14.png" width="40%" height="40%" title="70px" alt="memoryblock">　　<img src="https://user-images.githubusercontent.com/53032349/114357767-1b06a580-9bad-11eb-8372-e0251c75eb5b.png" width="50%" height="50%" title="70px" alt="memoryblock"></p>
