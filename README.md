## ❤️심전도 사용자인증 시스템

<p align="center">
  <img src="https://github.com/p-project6/p_p/assets/90545561/b8d8a290-8bdd-4c23-83f9-7d31c9f86924" width="50%"/>
</p>

## 📈프로젝트 개요   


<img width="400" alt="g" src="https://github.com/p-project6/p_p/assets/90545561/285d991c-006f-46fd-a306-1ba7ff551225">
<img width="403" alt="i" src="https://github.com/p-project6/p_p/assets/90545561/bbbab489-60f5-4df2-a359-bd8ccdfa2fc3">   

<p align="center">
  <b>사용자의 심전도를 측정하여 인증하는 모델 제작 프로젝트</b>
</p>   

> 사람은 개인마다 고유의 심전도를 가지고 있습니다. 따라서 지문이나 얼굴인식처럼 심전도를 측정하여 인증이 가능합니다. 이 점을 이용하여 심전도 사용자인증 시스템을 만들어 보았습니다.  


### 💻 사용기술   
- <img src="https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white">
- <img src="https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54">   
### 📆 프로젝트 기간
- 2023.11.22~2023.12.16   


## 🚩세부기능
### 1. 데이터   
<img width="520" alt="y" src="https://github.com/p-project6/p_p/assets/90545561/b651d924-184e-4785-96f6-42fde47e08a4">   

- 1명당 10초씩 60회 측정한 심전도 100명치
- 기본적으로 심전도 데이터는 주파수데이터 이므로 시계열데이터입니다. 따라서 전처리가 매우 중요합니다.
- 연속적인 데이터를 처리할 수 있는 모델을 구성해야 합니다.
- 원본 데이터를 그대로 사용할시 잡음이 많아 정확한 모델의 학습이 어려우므로 전처리 과정을 거칩니다.

### 2. 다운샘플링   
<img width="350" alt="g" src="https://github.com/p-project6/p_p/assets/90545561/285d991c-006f-46fd-a306-1ba7ff551225">       

- 첫 번째 전처리 작업으로 약 5만Hz였던 원본데이터를 256Hz로 낮추는 작업입니다.

### 3. 주파수통과필터      
<img width="500" alt="t" src="https://github.com/p-project6/p_p/assets/90545561/9a1344fa-5e97-4ff4-b6db-cf9658969b00">   

- 통과시킬 주파수의 범위를 정해 원하는 범위만 남기는 필터링 과정으로 3가지가 존재합니다.
- HighPassFilter는 설정값 이상의 주파수만 통과시키는 필터입니다.
- BandPassFilter는 일정 범위 안에 있는 주파수만 통과시키는 필터입니다.
- LosPassFilter는 설정값 이하의 주파수만 통과시키는 필터입니다.
- 필터링을 통해 필요없는 범위의 주파수는 날려줍니다.

### 4. 데이터분할
- 한 사람이 1회 측정한 데이터당 일정히 반복되는 주기가 존재합니다. 따라서 이를 토대로 데이터를 짧게 끊어 dataset의 양을 늘려줍니다.
- 기본적으로 1초씩 끊어서 데이터를 저장해주었습니다.

### 5. 모델적용
> 📢 모델   
> 1-dimensional CNN : 이다은   
> RNN : 채안나   
> LSTM : 이준형   
> GRU : 오수진   
- 저희는 모델 여러개를 각자 맡아 어떤 것이 가장 정확도가 높은지 실험을 진행하였습니다.   
<img width="320" alt="rnn" src="https://github.com/p-project6/p_p/assets/90545561/c2cc46f6-9e5b-4e5e-9221-02d4993069da">   

- RNN의 경우 SimpleRNN을 적용하였는데 학습하는 시간이 다른 모델에 비해 오래걸렸습니다.
- 정확도는 BandPass적용한 데이터가 약 91%정도 나왔습니다.


<img width="340" alt="lstm" src="https://github.com/p-project6/p_p/assets/90545561/f2e282dd-b800-4879-b42e-6e666dc3feda">   
<img width="300" alt="lstm-1" src="https://github.com/p-project6/p_p/assets/90545561/beb2f063-9f30-4ecd-91d3-9e9dc169c494">


- LSTM의 경우 시계열데이터에 자주 사용하는 모델이며 RNN보다 성능이 좋습니다.
- 그래프도 완만하게 나타났으며 정확도는 BandPassFilter를 사용하였을 때 98%로 가장 높았습니다.


<img width="336" alt="gru" src="https://github.com/p-project6/p_p/assets/90545561/a739b5ff-ca24-4f5a-b8bc-06ee4be0a579">
<img width="300" alt="gru-1" src="https://github.com/p-project6/p_p/assets/90545561/a5a400f2-f921-4988-9474-34a970b4ef5f">   


- GRU는 LSTM과 비슷하지만 비교적 빠른 모델입니다.
- 정확도 그래프는 LSTM보다 완만하며 정확도는 BandPassFilter사용시 94%정도로 나타났습니다.   


<img width="333" alt="cnn" src="https://github.com/p-project6/p_p/assets/90545561/ec67e6f6-c3d1-4afd-8f57-dc48b89b34f3">
<img width="300" alt="cnn-1" src="https://github.com/p-project6/p_p/assets/90545561/0bae99b9-9df7-425f-b1b9-7f46c73c69b0">   

- CNN모델은 짧은 구간에 대해서 패턴을 인식합니다.
- 정확도 그래프가 대체적으로 완만하나 Low그래프에서 변동이 있었습니다.
- HighPassFilter를 사용하였을 때 정확도가 99%로 가장 높게 나타났습니다.


### 결과적으로 CNN모델을 HighPassFilter를 이용해 학습시켰을 때 99%로 정확도가 가장 높았습니다.

### 6. 심화과정
> 가장 정확도가 높게 나온 CNN과 LSTM모델을 활용하여 추가적인 실험을 진행하였습니다.    
> 데이터를 2초로 분할, 겹쳐서 1초씩 분할한 경우를 추가로 시행해보았습니다.   
> 이중에선 겹쳐서 1초로 분할한 데이터를 bandpass에 적용시켜 CNN모델로 학습했을 경우가 98%정확도로 높게 나왔습니다.
> 심화과정까지 해본 결과 1초로 분할해 Highpass를 적용한 cnn모델이 99%로 가장 높았습니다. 


## 사용자 식별
<img width="403" alt="i" src="https://github.com/p-project6/p_p/assets/90545561/bbbab489-60f5-4df2-a359-bd8ccdfa2fc3">   

- testdata중 42번 사람의 데이터를 학습한 모델에 넣어본 결과 42번 사람으로 인식하는 것을 확인할 수 있습니다.
- 오른쪽 이미지의 경우 6000개의 testdata를 전부 모델에 적용시켜본 결과 거의 모든 데이터를 맞춘 것을 확인할 수 있습니다.
- 이를 애플워치나 갤럭시워치와 같이 심박수를 측정할 수 있는 전자기기에 활용하면 사용자를 인증하는 시스템을 만들 수 있습니다.



