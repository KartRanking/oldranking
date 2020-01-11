---
layout: page
title: About
permalink: /about/
---

카트라이더 리그 랭킹 블로그 v1.0

### TrueSkill 모형에 관하여
예전에 사용했던 Elo 모형은 근본적으로 1 대 1 게임만을 위한 모형이기 때문에 매 트랙마다 각 선수가 7개의 서로 다른 1 대 1 경기를 동시에 치른 것처럼 생각하여 계산했다. 예를 들어, 3위는 1,2위에게 패, 4-8위에게 승리하여 2승 5패를 동시에 한 것으로 처리했다. 반면, TrueSkill 모형은 그런 처리가 필요하지 않고, 8인 개인전, 4 대 4 팀전 등 다양한 시나리오에 맞춰 수학적으로 적절한 방식으로 적용이 가능하다. 이 모형은 각 선수의 시간에 따라 서서히 변하는 skill 값 s가 평균 mu, 표준편차 sigma의 정규 분포를 따른다고(베이지안 추론에서의 사전분포) 가정하고 선수가 각 경기에서 보여주는 performance p 는 평균이 s, 표준편차가 beta(권장되는 값은 (초기 sigma)/2. 이 블로그에서는 1000/2 = 500.)인 정규 분포를 따른다고 가정한다. 매 트랙마다 우리가 관측하는 것은 개인전의 경우 각 선수의 performance p의 순위, 팀전의 경우 각 팀의 p의 합이 어느 쪽이 큰 지이다. 랭킹 모형은 이 관측된 값을 토대로 approximate message passing이라는 방법을 통해 s의 사후 분포(경기 결과가 주어졌을 때의 s의 분포)를 계산한다. 계산된 사후 분포는 사전 분포와 마찬가지로 평균 mu’, 표준편차 sigma’를 따르는 정규 분포로 나타나고, 이 사후 분포를 이후 트랙에서 각 선수의 skill에 대한 사전 분포로 사용하게 되어 mu와 sigma를 점진적으로 업데이트해나가게 된다. (조금 더 정확하게는 시간에 따른 skill의 변화를 원활하게 추정하기 위해 다음 사전 분포의 분산을 약간 더 키워 주는 추가적인 파라미터 tau가 사용된다.)

이 블로그에 모든 모형에는 다음 파라미터가 사용된다:
초기 mu = 3000, 초기 sigma = 1000, beta = 500, tau = 10.

### 참고 자료

- [https://trueskill.org/](https://trueskill.org/): 분석에 사용된 패키지의 웹 문서.
- [http://papers.nips.cc/paper/3079-trueskilltm-a-bayesian-skill-rating-system.pdf](http://papers.nips.cc/paper/3079-trueskilltm-a-bayesian-skill-rating-system.pdf) Microsoft Research의 NIPS 2006 페이퍼.
- [http://www.moserware.com/2010/03/computing-your-skill.html](http://www.moserware.com/2010/03/computing-your-skill.html) Jeff Moser의 친절한 설명 블로그.
- [http://www.moserware.com/assets/computing-your-skill/The%20Math%20Behind%20TrueSkill.pdf](http://www.moserware.com/assets/computing-your-skill/The%20Math%20Behind%20TrueSkill.pdf) Jeff Moser의 TrueSkill의 수학적인 내용을 친절히 설명하는 페이퍼.


### Contact me

[kart.rider.ranking@gmail.com](mailto:kart.rider.ranking@gmail.com)
