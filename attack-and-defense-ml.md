# ML을 공격하는게 방어하는 것보다 쉬울까?

번역글 : [Is attacking machine learning easier than defending it?](http://www.cleverhans.io/security/privacy/ml/2017/02/15/why-attacking-machine-learning-is-easier-than-defending-it.html)

by Ian oodfellow and Nicolas Papernot || 번역 : 구글 번역기 + davinnovation

[첫 글](http://www.cleverhans.io/security/privacy/ml/2016/12/15/breaking-things-is-easy.html) - [번역]()에서, learning 과정 중 오염된 데이터를 넣거나, 잘못된 예측을 하도록 공격받은 데이터를 보여주는 방법으로 machine learning 시스템을 공격하는 방법을 보여드렸습니다. 이번 글에서는, 머신러닝 모델을 공격하는 것이 방어하는 것보다 왜 쉬운지 말씀드리려고 합니다. 음... 공격받은 데이터에 대한 효과적인 방어 방법을 왜 못 찾았고, 우리가 생각한 몇가지 방법을 보여드리겠습니다. 

Adverserial example(공격받은 데이터)는 머신러닝 모델에 넣게되면 틀린 예측 값을 나오게 하도록 디자인되었습니다. Panda 사진에 작은 방해를 더해서 Gibbon으로 인식하게 하는 방법이 대표적인 시작점입니다.

![images](http://cleverhans.io/assets/adversarial-example.png)


지금까지는, 위와 같이 모델을 속이지 못하게 방지하는 것보다는 속이는 것이 더 쉬웠습니다.

## 모델을 Robust하게 만들기...?

머신 러닝 모델을 Robust하게 하고 공격을 완화시킬 수 있는 방어 방법은 2가지, 'Adversarial Training'과 'Defensive distillation'가 있습니다.

### Adversarial Training

공격받은 데이터를 학습에 이용하여 prediction phase에서 잘 작동할 수 있도록 일반화 시키는 과정이다. 이 아이디어는 Szegedy[SZS13]에 의해 먼저 제시 되었으나, 공격받은 데이터를 생성하는 것은 높은 컴퓨팅 파워가 필요했기 때문에 실용적이진 못했다. Goodfellow가 fast gradient sign method를 통해 적은 컴퓨팅 파워로 효과적인 공격받은 데이터를 생성해낼 수 있게 하였다. 모델은 일반적인 데이터 + 공격받은 데이터 ( ex - 고양이 사진 + 공격받아 고양이가 사람으로 인식되는 사진)를 가지고 학습됩니다.

### Defensive distillation

공격자의 공격 방향을 통해 모델의 decision surface를 부드럽게 만드는 방법이다. Distillation는 전에 trained 된 모델을 다른 모델로 예측하기 위해 train을 진행하는 것을 말합니다. 이는 작은 모델로 컴퓨팅 파워가 큰 모델을 흉내내는 것이 목적이였습니다. Defensive distillation은 model을 smooth하게 만드는 것이 목표이고, 모델의 사이즈가 같더라도 작동이 되어야합니다. 하나의 모델의 output을 예측하는 같은 architecture를 가진 다른 model을 만드는 것은 비직관적으로 보입니다. 이를 달성하는 방법은 첫번째 모델은 hard label ( 100 % probability )를 주어 학습하고, 두번째 모델은 ( 95 % probability )를 주어 학습합니다. 두번째 모델은 distilled 되었다고 말할 수 있으며, 2번째 모델이 기존 모델보다 robust합니다. 

## 실패한 방어 전략 "gradient masking"

대부분의 공격은 model의 Gradient를 이용해서 이루어집니다. 쉽게 말하면, 비행기 사진을 보고 '고양이' class의 영역과의 방향을 계산 후 약간의 방향성을 더해줘서 비행기 사진을 고양이 사진으로 잘못 인식하도록 만드는 겁니다.

하지만 만약.... 'gradient'가 없다면 어떻까요? 이말은 즉슨, 공격자가 어디로 이미지의 방향을 줘야하는지 모르다는 의미입니다.

