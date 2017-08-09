# ML을 공격하는게 방어하는 것보다 쉬울까?

번역글 : [Is attacking machine learning easier than defending it?](http://www.cleverhans.io/security/privacy/ml/2017/02/15/why-attacking-machine-learning-is-easier-than-defending-it.html)

by Ian oodfellow and Nicolas Papernot || 번역 : 구글 번역기 + davinnovation

[첫 글](http://www.cleverhans.io/security/privacy/ml/2016/12/15/breaking-things-is-easy.html) - [번역]()에서, learning 과정 중 오염된 데이터를 넣거나, 잘못된 예측을 하도록 공격받은 데이터를 보여주는 방법으로 machine learning 시스템을 공격하는 방법을 보여드렸습니다. 이번 글에서는, 머신러닝 모델을 공격하는 것이 방어하는 것보다 왜 쉬운지 말씀드리려고 합니다. 음... 공격받은 데이터에 대한 효과적인 방어 방법을 왜 못 찾았고, 우리가 생각한 몇가지 방법을 보여드리겠습니다. 

Adverserial example(공격받은 데이터)는 머신러닝 모델에 넣게되면 틀린 예측 값을 나오게 하도록 디자인되었습니다. Panda 사진에 작은 방해를 더해서 Gibbon으로 인식하게 하는 방법이 대표적인 시작점입니다.

![images](http://cleverhans.io/assets/adversarial-example.png)


지금까지는, 위와 같이 모델을 속이지 못하게 방지하는 것보다는 속이는 것이 더 쉬웠습니다.

## 모델을 Robust하게 만들기...?