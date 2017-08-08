# 부수는건 쉬워요!

번역 : http://www.cleverhans.io/security/privacy/ml/2016/12/15/breaking-things-is-easy.html

by Nicolas Papernot and Ian Goodfellow || 번역 : 구글 번역기 + davinnovation

몇 년전만 하더라도, 머신러닝 알고리즘은 물체 인식, 번역 같은 의미있는 작업을 간단하게 수행하지 못했습니다. 머신러닝 알고리즘이 틀리는 것은, 예외라기 보다는 'RULE' 같은 것이였습니다. 오늘날, 머신러닝 알고리즘은 naturally occurring input으로도 human을 능가할 수 있을 정도로 발전했습니다. 머신러닝은 사소한 공격으로도 매우 성능이 떨어지기 때문에 아직은 실제 인간 수준의 실적은 내지 못합니다. 다른 말로는, 기계 학습이 작동하는 지점에 도달했지만 쉽게 깨질 수 있다는 겁니다.

이 포스트에서는 어떤 공격이 머신러닝 알고리즘을 망가트릴 수 있는지 논의할 겁니다. 좀 Academic하게 말해보자면 security and privacy of machine learning입니다. Ian과 Nicolas는 cleverhans 오픈 소스 프로젝트를 만들어 머신러닝의 취약성을 벤치마킹하고 있습니다. 

지금까지는, 대부분의 머신러닝은 아주 약한 위협(threat) 중에서 개발되어 왔습니다. 머신러닝 시스템은 자연스러운 상태에서 작동하도록 디자인 되었던 것이죠. 이제는, 공격적인 환경에서도 작동이 가능한 머신러닝 시스템을 디자인하고자 합니다.

