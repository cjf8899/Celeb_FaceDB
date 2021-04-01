# Create FaceDB
## Demo

Coming soon~


## 1. Crawling

* 코드 및 Visual Studio Code 다운, Python 다운
  * 크롤러 코드 다운 [WebCrawler_exe](https://github.com/cjf8899/WebCrawler_exe)
* 현재 chrome 버전 정보를 확인, 버전에 맞는 chromedriver를 다운
  * 자신의 크롬 버전을 찾고 chromedriver 다운로드
  * [크롬버젼 확인](chrome://settings/help)  
  * [chromedriver 다운](https://chromedriver.chromium.org/downloads)

<p align="center"><img src="https://user-images.githubusercontent.com/53032349/107145082-b64b8680-6982-11eb-8ee3-a71e026f92c3.PNG" width="90%" height="90%" title="70px" alt="memoryblock"></p>

## 2. 모델 개발 과정
 모델 개발 과정은 실험한 시간순으로 작성하였습니다.<br>
### 2.1. Baseline model
 먼저 주최 측에서 제공한 baseline 코드에는 3D-resnet(backbone)으로 구성되어있었고, 성능을 측정하고자 3D-resnet50, 3D-resnet101 둘 다 실험을 하였고 3D-resnet50이 **65%** 로 3D-resnet101보다 성능이 더 좋았습니다. 가벼운 테스크이다 보니 무거운 모델보다 가벼운 모델이 더 성능이 좋은 것 같습니다. lr, batch 등 hyperparameter은 실험할 때 loss, acc를 바탕으로 적용하였고 batch : 32, lr : 0.001로 픽스하였습니다.<br>
<br>
 이후, 기본 성능을 바탕으로 여러 가지 실험을 하였습니다. 첫 번째는 모델을 바꾸어 측정해보았습니다. baseline 코드에서 backbone을 R(2+1)D으로 변경하고 실험을 하였습니다. 이는 선배의 조언으로 바꾸었고, 간단한 테스크에서 R(2+1)D 좋을 수도 있다 하여 실험하였습니다. 결과는 **66 ~ 68%** 로 기본 baseline 코드보단 좋았습니다.<br>
<br>
### 2.2. 3D model
 다음은 backbone을 resnext로 변경하기 위해 노력하였습니다.<br>
(데이터로더 부분이 오류인줄알고 print 찍어보고, 이상한 오류 창을 몇 번이나 검색하였는데 알고 보니 preprocess_data 코드가 문제였음(리턴하는 부분이 빠져있어서 이미지? 데이터가 텐서나 노말라이즈 하지 못해 오류였음)
또한, 모델 fc부분에서 아웃풋 부분을 직접 모델 코드에서 변경하여 오류가 많았음(직접 건들지 말고 불러오는 코드로 건들자...))<br>
 따라서 주최 측의 baseline 코드 대신 [MARS](https://github.com/craston/MARS) 코드로 대체하였습니다.<br>
 그리고 요번 대회가 처음이라 pretrain model을 사용하면 안 된다고 알고 있었지만 사용해도 무관하다고하여 Kinetics pretrain model을 사용하였습니다. resnext50, 101 둘 다 실험하였고 resnext50이 **85%** 를 달성하였습니다. 50이 101보다 성능이 좋은 이유는 앞서 말한 이유와 마찬가지인 것 같습니다.<br>
<br>
 MARS의 resnext50에서 pretrain model을 사용하였고, 바로 전 실험은 마지막 layer와 마지막 fc만 fine tuning 하여 실험하였습니다. 하지만 예전에 transfer learning 논문을 읽었을 때는 전체를 fine tuning 하는 것이 더 좋은 결과를 얻은 기록이 있어 이번 실험에는 전 실험과 전부 동일하지만, 전체 fine tuning을 하는 실험을 하였습니다. 결과는 예상에 맞게 **87.5%** 성능이 더 좋았습니다.<br>
<br>
### 2.3. 2D model
 baseline 코드와 MARS 코드는 3D-model이다. 하지만 3D-model은 2D-model보다 무겁다. 또한, 간단한 테스크이니 2D를 사용해도 성능이 좋게 나올 것 같아 2D-model로 구현하였습니다. 2D-model는 3D-model 데이터로더와 다르기 때문에 수정하였고, 각 영상 프레임 중 랜덤하게 1장만 가져와 classification 하도록 만들었습니다. 모델은 resnet50을 사용하였고, imagenet pretrain을 사용하였습니다.<br>
결과는 최대 **91.3%** 를 달성하여 3D-model보다 훨씬 좋은 성능을 내었습니다. 이 전에 tiny imagenet challenge에서 과도한 transform보단 간단한 transform이 좋았기 때문에 RandomHorizontalFlip, RandomRotation만 사용하였습니다. 나중에 RandomRotation은 성능이 나오지 않아 제거하였습니다. 이유는 데이터 셋에서 사람이 넘어지는 경우의 라벨이 5개중 3개가 있고, RandomRotation이 넘어진 것을 모호하게 만드는 것 같았다.<br>

<p align="center"><img src="https://user-images.githubusercontent.com/53032349/107150249-43e99f00-69a0-11eb-90a8-0b0b21645ce0.PNG" width="80%" height="80%" title="70px" alt="memoryblock"></p>

<br>
 train, test dataset을 분석하였더니 마지막 프레임(대략 30%)정도는 관련이 없는 이미지라고 판단하여 마지막 프레임(30%)를 제외하고 나머지 70%만 사용하는 실험을 하였지만 성능은 같거나 오히려 더욱 떨어졌습니다. 이로 인해 모델이 카메라의 구도도 학습한다고 생각이 들었습니다.<br>
<br>
 위 실험과 동일한 세팅이지만 마지막 프레임(10%, 20%)을 제외하고 나머지 (90%, 80%) 만 사용하였지만, 결과는 이전과 동일하였습니다. 이후 SGD를 Adam으로 바꿔보는 등등 세세한 실험을 하였지만 성능은 같거나 떨어졌습니다.<br>
<br>
 3D-model에서는 이미지사이즈를 112로 고정시켜 2D-model에서도 112를 고정시켰지만 224, 448로 늘려감에 따라 실험하였고 **93%, 95.8%** 을 달성하였다. resnet50에서 다른 네트워크로 변경한 실험도 진행하였지만 성능이 비슷하거나 안 좋았다.<br>
<br>
 마지막으로 batch, lr, image size 등 hyperparameter를 적절히 조정하여 최고 성능인 **97.5%** 를 달성하였다.<br>
 <br>
 <p align="center"><img src="https://user-images.githubusercontent.com/53032349/107150378-dbe78880-69a0-11eb-93bc-3d98a22ecad3.PNG" width="70%" height="70%" title="70px" alt="memoryblock"></p>
 
 ## 성능 재현
 다음과 같은 프로세스를 통해 모델성능을 재현할 수 있습니다. 2D-model은 torchvision.models 를 사용하였기 때문에 따로 pretrained model이 필요없지만, 3D-model은 필요하기 때문에 성능 재현에 유의하십시오.<br>
 ```Shell
  python train2d.py --modality RGB --split 1 --only_RGB --n_classes 400 --n_finetune_classes 5 --batch_size 32 --log 1 --sample_duration 64 --model resnet --model_depth 50 --ft_begin_index 0  --result_path "results/" --n_workers 8 --n_epochs 100 --learning_rate 0.01
  
  or
  
  python train3d.py --modality RGB --split 1 --only_RGB --n_classes 400 --n_finetune_classes 5 --batch_size 32 --log 1 --sample_duration 64 --model resnext --model_depth 101 --ft_begin_index 0  --result_path "results/" --n_workers 8 --n_epochs 100 --learning_rate 0.01
 ```
