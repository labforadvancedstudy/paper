#  **Key-value memory in the brain** (2025.01.06)

arXiv:2501.02950v1 [q-bio.NC] 6 Jan 2025  

Samuel J. Gershman1,2,3,∗, Ila Fiete4, and Kazuki Irie2  
(1 하버드대학교 심리학과, 2 뇌과학센터, 3 자연 및 인공지능 연구를 위한 Kempner Institute, 미국 매사추세츠주 케임브리지, 4 매사추세츠 공과대학 McGovern 뇌연구소 및 뇌·인지과학과, ∗ 교신저자: gershman@fas.harvard.edu)

https://arxiv.org/abs/2501.02950

---

## **내용 설명**

이 논문은 “Key-value memory in the brain(뇌에서의 키-값 기억)”이라는 개념을 중심으로, 인공지능·심리학·신경과학을 아우르며 인간 뇌의 기억 메커니즘을 재조명합니다. 흔히 심리학·신경과학에서 사용되는 ‘유사성 기반’(similarity-based) 기억 모델은 “입력 단서가 메모리 패턴과 얼마나 비슷한가”를 기준으로 정보를 인출합니다. 하지만 이러한 모델만으로는 ‘저장’과 ‘인출’이 동시에 최적화된 구조를 충분히 설명하기 어렵습니다.

논문의 핵심은, **입력을 ‘키(key)’와 ‘값(value)’라는 서로 다른 두 가지 표현으로 변환하여 저장**하고, **‘인출할 때는 키와 질의(query)를 비교해 가장 관련 있는 값을 가중 결합하여 불러온다**는 새로운(혹은 강화된) 패러다임을 제시하는 것입니다. 이렇게 키와 값을 분리하면, 뇌가 기억하려는 정보(값)는 정확도를 높게 유지하면서도, 인출을 위한 주소(키)는 서로 명확히 구별되어 검색 충돌을 줄일 수 있습니다.

논문에서는 이 개념을 **현대 기계학습의 트랜스포머(transformer)나 빠른 가중치 프로그래머(fast weight programmer)** 같은 모델들과 연결해 설명하고, 심리학·신경과학의 여러 실험 결과도 이 틀에서 재해석합니다. 특히 ‘기억이 사라지는 것이 아니라 단지 불러오기(access)가 실패하는 것’이라는 주장을, 심리학적 관찰(오랜 기간 사용 안 한 기억도 어떤 계기로 다시 떠오를 수 있음) 및 신경과학적 발견(해마에 “침묵 상태”로 남아 있는 기억 흔적, 다시 활성화 시 기억 복구 가능)으로 뒷받침합니다.

- **해마(hippocampus)는 키(key)를 담당**, 즉 다양한 감각·에피소드·맥락 등의 정보를 **‘잘 분리 가능하고 검색 가능한 형태의 주소’**로 저장한다.
- **네오코텍스(neocortex)는 값(value)를 담당**, 즉 의미·지식·패턴 등의 실질적 내용물(semantic memory)을 저장한다.
- 인출 시에는 “질의(query) → 해마가 가진 키와 매칭 → 그 키와 연결된 값(네오코텍스)” 과정을 통해 기억을 끄집어낸다.

이러한 구조가 왜 중요한가?  
1) **저장 용량 문제**: 뇌가 가지고 있는 물리적 한계(뉴런과 시냅스의 수 등)는 분명 존재하지만, 실제로는 “신경망 어디에도 영구적으로 남아있다”는 식의 실험적·임상적 증거들이 많다. 기억은 지워지는 대신, 다른 기억들 간의 간섭(interference)으로 인해 접근 실패가 발생할 뿐이라는 것.  
2) **키-값 분리로 인한 최적화**: 검색(키)은 서로 간섭 없이 깔끔하게, 실제 정보(값)는 풍부하고 정확하게 표상함으로써, ‘구분도’와 ‘정밀도’를 동시에 달성한다.  
3) **“느낌”만 있고 내용은 기억 안 나는 현상**(tip-of-the-tongue, feeling of knowing 등)은 키-값 분리 구조를 잘 보여주는 예. 해마의 키 주소가 어떤 기억이 존재한다는 사실(‘있음’)만 인지하게끔 하지만, 정작 구체적인 내용(값)은 못 불러오는 상황.  
4) **신경학적 관찰**: 해마에 형성된 “침묵(또는 잠재) 엔그램(silent engram)”을 인위적으로 다시 활성화했을 때 과거 기억이 회복되는 사례 등은, 실제 뇌가 이런 식의 “묵혀둔 키”를 다시 이용해 값을 정상적으로 불러올 수 있음을 보여준다.

결론적으로, 저자들은 뇌에서 “키(key)-값(value)” 원리가 실제로 구현되어 있을 가능성이 높으며, 이것이 기계학습·신경과학·심리학적 연구를 새로이 통합할 수 있는 강력한 패러다임이라고 주장합니다.

---

## **핵심과 본질**

- **뇌 기억의 본질**:  
  - “기억은 지워지지 않고, 단지 못 찾게 될 뿐”이라는 오래된 가설을 더욱 정교화.  
  - 해마가 ‘키’를 만들어 검색 주소를 담당하고, 네오코텍스가 ‘값’을 담아 기억 내용의 정확성을 유지한다.  
  - 따라서 핵심은 **“올바른 키 주소를 찾으면 오래전에 축적된 값(기억)을 다시 불러낼 수 있다”**는 것.

- **기존 이론과 비교했을 때의 함의**:  
  - 고전적 유사성 기반 메커니즘만으로 설명하기 어려웠던 “감춰진 기억의 복원”과 “분명 존재하지만 인출 실패하는 현상”이, 키-값 분리로 말끔히 설명 가능.  
  - 또한, 뇌과학에서는 해마-신피질이 서로 상보적 학습 구조(episodic vs. semantic)라고 많이 말해 왔는데, 여기서 한 발 더 나아가 “해마=키/네오코텍스=값” 구조로 이해하면 기존 실험들(예: 해마 손상 시 특정 회상 능력만 사라짐 등)의 메커니즘이 더욱 정합적으로 해석됨.  
  - **AI와의 교차점**: 트랜스포머나 Hopfield 네트워크 등 “어텐션 기반” 딥러닝 구조도 사실상 키-값 메모리. 뇌 역시 진화적 차원에서 이런 메커니즘을 이미 구현해왔을 가능성이 높아 보임.

---

# 한글 번역

### **제목 및 초록**

**Key-value memory in the brain**  
(뇌에서의 키-값 기억)

arXiv:2501.02950v1 [q-bio.NC] 6 Jan 2025  
(2025년 1월 6일)

Samuel J. Gershman1,2,3,∗, Ila Fiete4, and Kazuki Irie2  
(1 하버드대학교 심리학과, 2 뇌과학센터, 3 자연 및 인공지능 연구를 위한 Kempner Institute, 미국 매사추세츠주 케임브리지, 4 매사추세츠 공과대학 McGovern 뇌연구소 및 뇌·인지과학과, ∗ 교신저자: gershman@fas.harvard.edu)

2025년 1월 7일

**Abstract**  
(초록)

고전적 심리학·신경과학의 기억 모델들은 “저장된 패턴과 인출 단서 사이의 유사도”를 기반으로 기억을 인출하며, 이 유사도는 단서와 저장된 패턴의 함수입니다. 이런 모델은 간결하지만, ‘저장’과 ‘인출’을 위한 표현이 구분되지 않는다는 문제가 있습니다. 이 둘은 계산적으로 다른 요구사항을 가지는데도 말이죠. 이에 비해 키-값 기억 시스템은, 저장에 사용되는 표현(값)과 인출에 사용되는 표현(키)을 구별합니다. 이는 키-값 메모리 시스템이 저장 충실도(fidelity)와 인출 구별도(discriminability)를 동시에 최적화할 수 있게 합니다. 우리는 키-값 기억의 계산적 기반, 현대 기계학습 시스템에서의 역할, 심리학 및 신경과학에서의 관련 아이디어, 다수의 실증적 난제에 대한 적용, 그리고 생물학적 구현 가능성 등을 검토합니다.

---

### **1 Introduction** (서론)

겉보기에는 기억이 매우 깨지기 쉽지만, 한 번 저장된 정보가 영구적으로 사라진다는 결정적 증거는 없습니다. 물론 뇌의 저장 용량이 유한하겠지만, 실제 기억 수행의 주요 제한 요인은 용량 자체가 아닌 “인출 과정”으로 보입니다. 즉, 관련 정보가 뇌 어딘가에는 남아 있지만, 항상 그것을 찾을 수 있는 것은 아닌 겁니다(Tulving, 1974; Crowder, 1976; Lewis, 1979; Miller, 2021). 이를 지지하는 증거를 아래에서 요약합니다.

인출 중심 관점에서 보면, 기억 수행의 핵심 설명 부담은 “기억이 어떻게 어드레싱(addressing)되는가(즉, 인출 시스템이 저장 위치를 어떻게 추적하는가)”와 “어떻게 질의(단서)를 저장된 정보 주소로 매핑하는가”에 놓이게 됩니다. 이런 개념에 대한 인지심리학·신경과학적 이론은 오랜 역사를 가집니다(Kahana, 2012; Chaudhuri and Fiete, 2016). 최근 기계학습 분야에서도 이와 유사한 분석이 발전하여, 트랜스포머나 빠른 가중치 프로그래머(fast weight programmer) 같은 고성능 시스템의 토대가 되었습니다(Vaswani et al., 2017; Schmidhuber, 1992). 자연 지능과 인공 지능 모두에서 “효과적인 정보 인출”이 지능의 중요한 측면이라는 인식이 커지고 있습니다(Graves et al., 2016; Gershman and Daw, 2017; Geva et al., 2021; Irie et al., 2022; Allen-Zhu and Li, 2024).

우리의 목적은, 심리학·신경과학·기계학습에서 논의되는 기억 인출 개념을 서로 연결하는 것입니다. 이를 위해 핵심 개념인 **키-값 기억(key-value memory)**을 도입합니다. 기본 아이디어는 다음과 같습니다: 입력(기억할 것)을 두 종류의 서로 다른 표현, 즉 ‘키(key)’와 ‘값(value)’로 변환해 함께 저장합니다. 키는 메모리 주소를, 값은 메모리 내용을 나타냅니다. 기억을 인출할 때는 먼저 ‘질의(query)’를 각 키에 대조하고, 그 결과가 유사한 키들의 값을 가중 결합하여 최종적인 기억을 읽어옵니다. 중요한 점은, **키와 값을 만드는 매핑이 별도로 최적화될 수 있다**는 사실입니다. 즉 “어떻게 찾을지(키)”와 “무엇을 담을지(값)” 정보를 구분해 설계함으로써, 인출 효율과 저장 충실도를 동시에 잡을 수 있습니다. 이는 인류가 설계해 온 정보 검색 시스템과 비슷합니다. 예를 들어, 책 뒤편에 있는 찾아보기 색인은 “해당 항목이 몇 페이지에 있느냐”만 알려주고, 항목의 실제 의미 내용은 담지 않습니다. 우리는 색인을 통해 해당 페이지를 찾아가야 책의 실제 내용(값)을 읽어볼 수 있죠.

우리는 뇌 메모리도 비슷한 원리를 따른다고 주장합니다. 특히, 해마(hippocampus)가 ‘키’를, 신피질(neocortex)이 ‘값’을 저장하는 분업 구조가 존재한다고 봅니다. 이와 유사한 아이디어는 이미 심리학·신경과학 분야에서 제안되어 왔으며, 키-값 메모리 틀로 연결 지으면 뇌 기억의 계산적 강점을 더 잘 이해할 수 있습니다. 이를 보여주기 위해, 특정 실험 현상을 재현하는 시뮬레이션을 제시합니다. 마지막에는 자연 지능과 인공 지능의 융합 관점에서 시사점을 논의합니다.

---

### **2 Computational foundations of key-value memory**  
(키-값 기억의 계산적 기반)

이 장에서는 키-값 기억을 뒷받침하는 기술적 아이디어를 소개하며, 다양한 개념화 방식을 살펴봅니다. 또한 현대 기계학습 체계에서 키와 값 표현을 어떻게 학습할 수 있는지, 고정(혹은 부분적으로 고정)된 “스캐폴드(scaffold)” 키 표현과 엔드 투 엔드로 학습하는 접근법을 비교해 봅니다.

---

#### 2.1 From correlations to kernels  
(상관에서 커널로)

키-값 메모리의 초기 형식화를 보여주는 대표적 예시가 코호넨(Kohonen, 1972)의 상관행렬 기억 모델(correlation matrix memory)입니다. 파이크(Pike, 1984)가 이를 활용해 여러 인간 기억 현상을 설명했는데, 여기서는 기호와 용어를 조금 바꿔 최근 모델과 맥락을 맞춰보겠습니다(그림 1 왼쪽). 각 입력 n은 키 벡터 \(\mathbf{k}_n\)과 값 벡터 \(\mathbf{v}_n\) (여기서는 행 벡터)로 구성됩니다. 직관적으로, 키는 메모리 주소(address) 정보를 담고, 값은 실제 기억 콘텐츠를 담습니다. 이 둘을 연결해 주는 ‘어소시에이터(associator)’ 행렬 \(\mathbf{M}\)은 초기값이 0이고, 매 입력을 받을 때마다 키 벡터와 값 벡터의 외적을 더해 갱신됩니다:

\[
\Delta \mathbf{M} \propto \mathbf{k}_n^\top \mathbf{v}_n.
\tag{1}
\]

이는 키 유닛과 값 유닛 사이에서 동시에 발화가 일어날 때 시냅스 강도가 증가한다는 고전적 Hebbian 학습을 그대로 따른 형태입니다(Caporale and Dan, 2008). 실제 뇌에서 학습은 훨씬 복잡하지만, 여기서는 식 (1)의 생물학적 개연성을 가정합니다(참고: Limbacher and Legenstein, 2020은 이와 유사하되 좀 더 복잡한 규칙을 제안).

이 상관행렬 기억은 **헤테로연상(heteroassociative)** 구조로, 서로 다른 종류(키와 값)의 객체/특성 간 관계를 저장합니다(Steinbuch and Piske, 1963). 만약 키와 값을 동일하게 두면, 오토연상(자동연상) 기억(autoassociative memory)이 됩니다(Willshaw et al., 1969; Anderson, 1970; Amari, 1972; Nakano, 1972). 이는 흔히 홉필드 네트워크(Hopfield network)로 불리는 모델(Hopfield, 1982)의 기반이기도 합니다.

상관행렬 기억에서 인출은, 어소시에이터 행렬 \(\mathbf{M}\)에 질의 벡터 \(\mathbf{q}\)를 내적하는 방식으로 이뤄집니다:

\[
\hat{\mathbf{v}} = \mathbf{q}\mathbf{M}.
\tag{2}
\]

신경회로망 관점에서는, 키 유닛에 질의 \(\mathbf{q}\)를 활성화하면, 학습된 시냅스(\(\mathbf{M}\))를 통해 값 유닛에서 출력 벡터 \(\hat{\mathbf{v}}\)가 생기는 형태입니다. \(\hat{\mathbf{v}}\)는 저장된 값 벡터들의 가중합이 되는데, 여기서 가중치는 “질의와 키의 유사도”에 의해 결정됩니다. 이를 “이중(dual) 형식”으로 쓰면 더 분명해집니다(Ba et al., 2016; Katharopoulos et al., 2020):

\[
\hat{\mathbf{v}} \propto \sum_{n=1}^{N} \alpha_n \mathbf{v}_n,
\tag{3}
\]

여기서 \(\{\alpha_n\}\)은 \(\alpha = \sigma(S(\mathbf{K}, \mathbf{q})) = \mathbf{q}\mathbf{K}^\top\)로 계산된 “어텐션 가중치” 세트이며, \(\mathbf{K}\)는 모든 키 벡터(행 단위 \(\mathbf{k}_n\))를 모은 행렬입니다. 함수 \(S(\cdot,\cdot)\)는 키와 값을 매칭하는 ‘유사도 커널(지금은 선형)’이고, \(\sigma(\cdot)\)는 분리 연산자(현재는 항등함수)입니다. 즉, \(\hat{\mathbf{v}}\)는 저장된 값 \(\mathbf{v}_n\)들의 가중합이고, 그 가중치는 “질의와 각 키의 유사도”로 결정됩니다.

이 이중 형식은, 모델을 일반화하는 데에도 유용합니다. 양의 반정부호(positive semidefinite) 커널이라면, 어떤 벡터 공간에서의 내적으로 표현 가능하므로(Schölkopf, 2002), 선형 외에도 다양한 유사도 함수를 정의할 수 있습니다. 예컨대 RBF 커널 등을 사용할 수도 있습니다(Tsai et al., 2019). 또한 주목할 점은, 이 일반화된 상관행렬 기억이 **트랜스포머(transformer)**의 셀프 어텐션과 같은 구조를 구현할 수 있다는 겁니다(Vaswani et al., 2017):

\[
S(\mathbf{K}, \mathbf{q}) = \frac{\mathbf{q}\mathbf{K}^\top}{\sqrt{D}},
\tag{5}
\]

\[
\sigma(\tilde{\alpha}) = \frac{\exp(\tilde{\alpha})}{\sum_n \exp(\tilde{\alpha}_n)},
\tag{6}
\]

여기서 \(D\)는 키/값 벡터의 차원수, 소프트맥스 함수를 분리 연산자로 쓴 예입니다. 분리 연산자를 항등함수로 둔 경우(\(\sigma(\cdot)\)가 항등)는 선형화된 어텐션(linearized attention)이 되고(Katharopoulos et al., 2020), 이는 재귀형 신경망(RNN)의 한 형태인 ‘fast weight programmer’(Schmidhuber, 1992; Schlag et al., 2021)와 동등하게 표현될 수 있습니다. 단, 소프트맥스 어텐션은 병렬 처리가 가능하지만 시퀀스 길이에 대해 계산 복잡도가 제곱적(quadratic)이 되고, 선형화된 어텐션은 순차적(recurrent) 처리로 선형 복잡도를 지니게 되는 식의 장단점 교환이 있습니다(Choromanski et al., 2021; Peng et al., 2021).

Millidge et al.(2022)는, 커널과 분리 함수의 다양한 선택에 따라 고전적 여러 기억 모델이 동일 틀에서 재파악될 수 있음을 보였습니다. 예컨대 **sparse distributed memory**(Kanerva, 1988)는 \(\sigma(\cdot)\)를 임계(threshold) 함수로 설정함으로써, **dense associative memory**(Krotov and Hopfield, 2016)는 \(\sigma(\cdot)\)를 정다항식(rectified polynomial)으로 설정함으로써 얻어집니다. 잡음이 없는 환경에서는, 이상적인 분리 함수는 \(\max\) 연산이 되어, 항상 정확히 일치하는 키의 값을 반환하게 됩니다(Millidge et al., 2022). 그러나 이는 잡음에는 취약합니다. 또한 새로운 입력에 대한 일반화를 위해서는 완벽 일치가 목표가 아닐 수도 있습니다(Vaswani et al., 2017; Ramsauer et al., 2021; Bricken et al., 2023). 예컨대 키-값 메모리는 Q&A(question-answering) 작업(Sukhbaatar et al., 2015; Miller et al., 2016)에서 널리 쓰이며, 질의 \(\mathbf{q}\)가 ‘질문’을, 값 \(\mathbf{v}\)가 ‘답’을 나타냅니다. 시스템은 “질문-답” 쌍들의 집합을 저장하고, 새로운 질문에 맞춰 적절한 답을 인출하려 하죠.

---

#### 2.2 Representational structure  
(표현 구조)

지금까지는 키, 값, 질의를 시스템에 그대로 제공받는다고 가정했습니다. 하지만 실제 현대 기계학습에서는 이들을 입력 벡터 \(\mathbf{x}_n\)로부터 특정 매핑을 통해 얻는 식으로 구성하는 경우가 많습니다. 트랜스포머나 빠른 가중치 프로그래머에서는 보통 아래와 같은 선형 함수를 가정합니다:

\[
\mathbf{k}_n = \mathbf{x}_n \mathbf{W}_k,
\tag{7}
\]

\[
\mathbf{v}_n = \mathbf{x}_n \mathbf{W}_v,
\tag{8}
\]

\[
\mathbf{q}_n = \mathbf{x}_n \mathbf{W}_q,
\tag{9}
\]

여기서 \(\{\mathbf{W}_k,\mathbf{W}_v,\mathbf{W}_q\}\)는 학습되는 가중치 행렬들이고, \(\mathbf{x}_n\)은 (원시 입력 데이터를 심층 학습으로 임베딩한) 입력 벡터일 수 있습니다.

일부 시스템에서는 키와 질의 매핑을 고정(random하게 혹은 어떤 구조적으로) 시키고, 값 매핑만 학습하기도 합니다. 이런 시스템에서는 주소 공간(address space)을 일종의 ‘스캐폴드’로 보고, 내용 정보와는 무관하게 주소만 배정해 둡니다. 예를 들어, **sparse distributed memory**(Kanerva, 1988)에서는 주소 스캐폴드가 임의(random)로 설정되어, 유사한 키가 유사한 값을 굳이 가리키지 않도록 합니다. 이는 디지털 컴퓨터의 RAM 접근 구조와 비슷한 면이 있죠.

반면, **Hopfield 네트워크**(Hopfield, 1982)나 관련 자동연상 기억 모델에서는 키와 값이 동일하므로 ‘콘텐트 주소화(content addressability)’를 자연스럽게 구현하게 됩니다(Kohonen, 1980). 이는 심리학·신경 모델에서도 흔히 채택됩니다.

또 어떤 모델들은, 무작위로 주소를 부여하되 이 주소가 시간에 따라 서서히 바뀌게 하여, 시간적으로 인접한 입력들은 주소 공간에서도 유사한 키로 인코딩되도록 합니다. 단순 시계열 상관만으로도, 인간·동물의 여러 기억 현상을 설명할 수 있다는 것이지요(Landauer, 1975; Estes, 1955).

뒤에서 고정 스캐폴드 기반의 신경영감(neurobiologically inspired) 아키텍처가 학습형보다 뛰어날 수도 있음을 보여줄 것이고, 반대로 키와 질의 매핑까지 학습해 “힙포캠퍼스 표현에서의 반발(repulsion) 효과” 같은 현상도 설명할 수 있음을 시뮬레이션으로 보일 겁니다. 뇌가 정말 이 둘을 혼합해 쓰는지, 이런 방식이 기계학습에서도 유용한지 등은 향후 과제로 남아 있습니다.

---

#### 2.3 The ubiquity of key-value memory  
(키-값 기억의 보편성)

지금까지는 키-값 기억을 명시적으로 구축한 예만 봤지만, **다른 모델들도 사실상 키-값 기억과 동등**한 경우가 종종 있습니다. Irie et al.(2022)는, **선형 계층(linear layer)을 경사하강법으로 학습하는 신경망**도 동일하게 해석할 수 있음을 보였습니다.

입력 벡터가 \(\mathbf{x}_n\)이고, 선형 계층의 출력이 \(\mathbf{y}_n = \mathbf{x}_n \mathbf{W}\)라고 합시다. 여기서 \(\mathbf{W}\)는 경사하강법으로 학습되는 가중치 행렬입니다. \(N\)번의 학습 스텝 후,  
\[
\mathbf{W} = \mathbf{W}_0 + \sum_{n=1}^{N} \mathbf{x}_n^\top \mathbf{e}_n,
\tag{10}
\]
이 되는데, \(\mathbf{W}_0\)는 초기 가중치, \(\mathbf{e}_n = -\eta_n (\nabla_{\mathbf{y}} L)_n\)은 러닝 레이트 \(\eta_n\)과 손실 \(L\)에 대한 오차 항입니다.

Irie et al.(2022)는 이 구성이 **아래처럼 표현되는 키-값 메모리**와 동일한 출력(같은 \(\mathbf{y}\))을 만든다고 지적합니다:

\[
\mathbf{y} = \mathbf{x}\mathbf{W}_0 + \sum_{n=1}^{N} \alpha_n \mathbf{v}_n,
\tag{11}
\]
여기서(우리가 쓰던 표기로) \(\alpha = \mathbf{q}\mathbf{K}^\top, \mathbf{v}_n = \mathbf{e}_n, \mathbf{k}_n = \mathbf{x}_n, \mathbf{q} = \mathbf{x}\)가 됩니다. 즉 선형 계층은 학습 과정에서 접한 오차 패턴을 모두 기억하며, 새로운 입력에 대해 그 기억의 선형 결합을 출력으로 내놓는 형태로 작동합니다. 인간 기억 연구에서 “오류가 오히려 더 또렷이 기억된다”는 현상(작업·오류가 학습에 중요한 역할을 함)과도 일맥상통합니다(Green, 1956; Hirshman et al., 1989; Sakamoto and Love, 2004; Rouhani et al., 2018; Bein et al., 2021).

이 선형 계층은 모든 학습 입력을 절대 “잊지” 않습니다(Irie et al., 2022). 단, 인출 접근이 일시적으로 차단될 수 있을 뿐입니다. 아래 심리학·신경과학 논의에서 다시 살펴봅니다.

---

### **3 Neurobiological substrates**  
(생물학적 기제)

키-값 기억은 뇌에서 어느 정도 영감을 받은 것이지만, 실제로 이를 생물학적으로 어떻게 구현할 수 있는지는 미해결 과제입니다. 식 (1) 같은 규칙은 (어느 정도) 생물학적으로 개연성이 있다고 쳐도, 키와 값 자체를 저장·학습하는 규칙도 필요하죠. 2장 ‘표현 학습’에서 설명한 것처럼, 현대 기계학습에서는 \(\{\mathbf{W}_k, \mathbf{W}_q, \mathbf{W}_v\}\)를 역전파(backpropagation)로 학습하지만(Lillicrap et al., 2020), 뇌에서 그런 메커니즘이 그대로 구현되는지는 불분명합니다.

이와 별개로, Tyulmankov et al.(2021)은 **키 학습**을 위한 비-Hebbian 규칙을 제안합니다. 이들은 키-값 메모리를 세 개 층으로 구성된 신경망(입력 \(\mathbf{x}\) → 히든층 \(\boldsymbol{\alpha}\) → 출력층 \(\hat{\mathbf{v}}\))으로 본 뒤(그림 1 오른쪽), 히든 유닛 각각이 “한 개(혹은 몇 개)의 입력”을 할당받도록 설계합니다. 이때 **키 행렬 \(\mathbf{K}\)**는 입력-히든 시냅스 가중치, **값 행렬 \(\mathbf{V}\)**는 히든-출력 시냅스 가중치에 해당합니다. 저자들이 제안한 히든층 시냅스 업데이트 규칙(단순화 버전, 시간지수 생략)은:

\[
\Delta K_{ij} \propto \mu \gamma_i (x_j - K_{ij}),
\tag{12}
\]

여기서 \(\mu\in \{0,1\}\)는 전역적 ‘3차 요인’(신경조절물질 같은 역할), \(\gamma_i\in \{0,1\}\)는 국소적 ‘3차 요인’(데드릭(수상돌기) 스파이크 같은 역할)입니다. 이 \(\gamma_i\)는 “가장 최근에 사용되지 않은” 히든 유닛을 가리키도록 설정되어, 키 학습에 있어 희소성(sparsity)을 유도합니다. 저자들은 이 규칙이 해마에서 관찰된 ‘행동 시간 척도 가소성(behavioral time scale plasticity, Bittner et al., 2017)’과 유사하다고 말합니다. 키 학습이 해마에서 일어날 가능성을 이 장 후반부에서 더 논의할 것입니다.

값 학습에 관해서는, Tyulmankov et al.(2021)이 “출력층을 목표 값 \(\mathbf{v}\)으로 클램핑(clamping)하고”, 히든-출력 시냅스 \(\mathbf{V}_{mi}\)를 다음 규칙으로 학습시킨다고 말합니다:

\[
\Delta V_{mi} \propto \mu \gamma_i \alpha_i (v_m - V_{mi}).
\tag{13}
\]

이는 히든 유닛과 출력 유닛의 동시활성에 기반한 **Hebbian 규칙**입니다. 해마 영역 CA1에서 내후각(entorhinal cortex)으로 투사되는 출력 시냅스의 변화 과정을 설명할 수도 있겠습니다.

Kozachkov et al.(2023)은 또 다른 구조를 제안했는데, **‘삼부신경합치(tripartite synapse)’**라 불리는 전(前)시냅스 뉴런-후(後)시냅스 뉴런-성상교세포(astrocyte)로 이뤄진 구조를 가정합니다. 특히 이들은 키-값 메모리의 세 층 가운데 ‘히든-출력’ 시냅스를 이 삼자 시냅스가 담당한다고 봅니다. 각 성상교세포 돌기가 히든 유닛 활성의 선형함수로 모델링되며, 이들이 집단적으로 \(\mathbf{S}(\mathbf{K}, \mathbf{q})\) 유사도 함수를 계산한 뒤, 히든-출력 가중치를 곱셈 방식으로 조정해 트랜스포머의 셀프-어텐션을 구현한다는 식입니다.

---

#### **Box 1: Random projections of attractor states for error-correcting key-query matching**  
(박스 1: 에러 보정 키-질의 매칭을 위한 끌개(attractor) 상태의 무작위 투영)

Vector-HaSH(Chandra et al., 2023)와 MESH(Sharma et al., 2022)는 삼중망(tripartite network) 구조로, 입력(감각) 층, 밀집 연결된 층, 그리고 “모듈형 고정점(끌개) 네트워크” 층으로 구성됩니다. 이 모델들은 키-질의-값 구조와 직결될 수 있습니다. 즉, 삼중망 가중치를 \(\mathbf{W}_{sd}, \mathbf{W}_{da}, \mathbf{W}_{ad}, \mathbf{W}_{ds}\)라 하고(각각 감각→밀집, 밀집→끌개, 끌개→밀집, 밀집→감각), 끌개 층 상태 \(\{a\}\), 밀집층 상태 \(\{d\}\), 감각층 상태 \(\{s\}\)라 합시다. 밀집층 반응이 선형이라고 보면(실제로는 비선형임), 아래 연산을 수행합니다:

\[
\hat{s} = \phi(s \mathbf{W}_{sd}\mathbf{W}_{da}, \{a\}) \mathbf{W}_{ad}\mathbf{W}_{ds},
\]

여기서 \(\phi(\cdot,\cdot)\)는 끌개층의 최근접 이웃(NN) 연산을 효율적으로 수행해 감각 입력 \(s \mathbf{W}_{sd}\mathbf{W}_{da}\)와 가장 가까운 끌개 상태 \(\{a\}\)를 찾는 함수입니다. 이 모델은 그림 1(B)의 키-값 시스템으로 해석될 수 있는데, 끌개층 출력 \(\mathbf{a}\)를 (잡음 제거된) 질의 \(\mathbf{q}_n\)으로 보고, \(\mathbf{W}_{ad}\)와 \(\mathbf{W}_{ds}\)가 각각 키와 값 행렬(\(\mathbf{K} = \mathbf{W}_{ad}^\top, \mathbf{V} = \mathbf{W}_{ds}\)) 역할을 합니다. 즉 숨겨진 히든 상태(어텐션 가중치)는 \(\alpha_n = x_n \mathbf{W}_{ad}\). 전체적으로 이 모듈형 끌개망이 \(\sigma(S(\mathbf{K}, \mathbf{q}))\)를 계산하고, 출력 \(\hat{\mathbf{v}} = \alpha_n \mathbf{W}_{ds}\)를 만들어 내는 셈이죠.

MESH와 Vector-HaSH는 기억 값을 감각 입력층에서 재구성하며, 학습은 Hebbian 방식으로 진행됩니다. 예컨대 \(\mathbf{W}_{sd} = n_s^\top n_d^n\), \(\mathbf{W}_{ds} = n_d^\top n_s^n\) 같은 식으로 밀집-감각 방향 가중치를 학습하되, \(\mathbf{W}_{da}\)와 \(\mathbf{W}_{ad}\)는 무작위 고정(또는 의사역행렬)으로 둡니다. 이렇게 키는 랜덤·고정 형태가 되고, 모듈형 끌개 상태를 통해 키가 잘 분리·보정되어 잡음에도 강인해집니다.

흥미로운 점은, 이 방식이 전형적 기억 모델에 등장하는 “기억 절벽(memory cliff)”—즉, 저장 용량 한계를 넘으면 기억 성능이 갑자기 추락하는 현상(Amit et al., 1987; McCloskey and Cohen, 1989)—을 피하고, 사람이 보여주는 완만한 망각(중첩 주소로 인한 간섭)의 형태를 재현할 수 있다는 것입니다(Barnes and Underwood, 1959). 실제로 MESH와 Vector-HaSH는, 단순 재구성 오차 최소화를 목표로 학습하는 유연한 인코더(Radhakrishnan et al., 2020)보다도 성능이 좋았습니다. 이는 **내후각-해마 체계가 진화에 의해 발견된 매우 효율적인 기억 주소화 시스템**일 가능성을 시사합니다.

Vector-HaSH는 2차원 격자(예: 그리드 셀 활동) 같은 기하학적 구조를 사용해, 이산 항목이든 연속 공간에서 배치된 항목이든, 순차적 에피소드(시간 연속)든 공간 기억(공간 연속)이든 상관없이 잘 처리할 수 있게 설계되었습니다.

---

### **4 Evidence from psychology and neuroscience**  
(심리학 및 신경과학적 증거)

이번 장에서는 뇌가 키-값 기억을 구현한다고 볼 만한 여러 근거를 검토합니다. 이는 다음 네 가지 주장과 연관됩니다:

1. 기억은 일단 저장되면 쉽게 사라지지 않고, 인출 간섭으로 인해 접근이 제한된다.  
2. 기억은 인출(키) 표현과 내용(값) 표현이 분리되어 있으며, 키는 구별력(서로 다른 기억을 확실히 분리) 중심으로, 값은 정보 정확도 중심으로 최적화되어 있다.  
3. 키에 담긴 정보는 의식적 접근(회상)에 직접적으로 제공되지 않는다. 뇌는 키로 값을 찾아오지만, 그 키 자체는 우리가 “기억했다”고 말하기 어렵다.  
4.1절에서 이 중 첫 번째를 다루고, 이어서 차례대로 살펴봅니다.

---

#### 4.1 Retrieval interference, not erasure, is the principal limiting factor in memory performance  
(인출 간섭, 즉 방해가 기억 수행의 주요 제한 요인이지, 실제 ‘소거’가 아니다)

키-값 기억 모델에서 시사하듯, 기억 성능은 “저장 용량”이 아니라 “인출을 얼마나 잘 해내느냐”가 관건입니다. 여기서는 뇌가 충분한 저장 능력을 지니고 있고, 실제로는 retrieval failure(인출 실패)가 망각의 주요 원인이라는 주장에 대한 근거를 살펴봅니다.

뇌의 물리적 용량을 추산하려는 시도는 많았지만(Dudai, 1997), 뉴런 수, 시냅스 연결 등을 근거로 대략 10^7~10^15비트 사이 추정치가 나오고, 감각계 입력량은 10^13~10^17 정도로 추산됩니다. 어느 정도 압축을 거친다면 저장 한계가 근본적 병목은 아닐 수 있다는 결론도 나옵니다.

더 설득력 있는 건, **행동 관찰**입니다. 저장 용량이 꽉 찼다면 새로운 정보를 저장하기 위해 오래된 정보를 영구 삭제해야 할 텐데, 인간은 수십 년 전에 배운 것도(오래 복습 안 해도) 부분적으로나마 기억해냅니다(Bahrick et al., 1975; Bahrick and Hall, 1991; Conway et al., 1991; Maxcey et al., 2021). 만일 진짜로 용량이 찼다면, 훨씬 빠른 시기에 과거 기억이 대거 사라져야 할 겁니다.

또, 짧은 시간 규모의 실험에서도 “리스트 기억”을 보면, 리스트 길이가 길수록 회상률이 떨어지지만 보통 5~20개 단어 수준에서 발생합니다. 이걸 “저장 공간 부족”으로 설명하긴 어려운데, Shiffrin(1970)의 연구에서는 여러 리스트를 차례대로 보여준 뒤, “가장 최근 리스트가 아닌, 바로 직전에 본 리스트”를 회상하도록 하면, 정작 그 직전에 본 리스트의 길이는 기억력에 별로 영향을 주지 않았고, 회상 대상인 리스트의 길이가 핵심 요인이었습니다. 이는 오래된 리스트가 새 리스트에 의해 “치환”되거나 “제거”되지 않았음을 시사합니다. 더 중요한 건 “동일 리스트 내 다른 항목과의 간섭”이죠.

Berens et al.(2020)은 단어-위치 쌍을 기억시키는 과제를 통해, “접근성(accessibility)”과 “정확도(precision)”를 분리 측정했습니다. 시간이 지날수록 접근성은 떨어졌지만, 회상에 성공했을 때의 정확도 자체는 별로 떨어지지 않았습니다. Diamond et al.(2020)의 실험도 같은 결론을 냈습니다. 즉, **한 번 사라진 기억이라 여겨졌던 것도, 다시 떠오르면 여전히 선명**하다는 겁니다.

“잃어버린 줄 알았던 기억”도 **적절한 단서**나(Roediger and Thorpe, 1978; Wagenaar, 1986) **여러 번 시도**(Buschke, 1974) 또는 **충분히 긴 시간 경과**(Payne, 1987) 뒤에는 다시 인출될 때가 있습니다. 심지어, 인공적으로 유도된 역행성 기억상실(약물, 뇌 손상 등)도 시간이 지나거나 특정 조건에서 복원되는 사례가 흔합니다(Kapur, 1999; Lewis et al., 1968; Riccio and Richardson, 1984; Miller, 2021). 예컨대 단백질 합성 억제 약물로 조건형성을 없앤 것처럼 보여도, 며칠 뒤 테스트하면 다시 나타나거나(Flexner et al., 1966; Serota, 1971; Squire and Barondes, 1972), **역설적으로 그 약물을 다시 투여**하면 기억이 되살아나는 경우도 있습니다(Bradley and Galal, 1988; Briggs and Olson, 2013; Gisquet-Verrier et al., 2015).

이와 유사하게, 고전적 조건형성에서 소거(extinction) 이후에도 **스스로 저절로(spontaneous) 반응이 되살아**나거나(Pavlov, 1927), 무심결에 ‘리마인더’ 자극으로 쉽게 복원(Rescorla and Heth, 1975)되는 현상도 결국 저장 자체가 사라진 것이 아니라 인출 경로만 막힌 것으로 보입니다.

종합해 보면, 다양한 증거들이 “잊어버림 = 불가역적 소거”가 아니라 “인출 실패”라는 관점에 힘을 실어줍니다. 실제로 저장된 기억도 간섭이나 단서 부재로 인해 찾을 수 없을 뿐, 필요 조건을 갖추면 다시 회복될 수 있다는 것입니다. 5.2절에서 이를 모델 시뮬레이션으로 보이겠습니다.

---

#### 4.2 Distinct representations of keys and values  
(키와 값의 분리된 표현)

“상보 학습 시스템(Complementary Learning Systems)” 이론에서는 해마가 **에피소드 기억**, 신피질이 **의미 기억**을 담당한다고 봅니다(McClelland et al., 1995; O’Reilly and Norman, 2002). 여기서는 해마가 구체적 시간·장소 맥락을 담는 “삶의 사건(episodic)”에 특화되고, 신피질은 여러 에피소드에서 공통 추출된 규칙·패턴(semantic)에 특화된다고 주장합니다. 이 패러다임은 AI 시스템에도 영감을 줬습니다(Kumaran et al., 2016).

우리는 여기서 더 나아가, **해마가 “값” 자체를 저장한다기보다, “키”를 저장하여 신피질의 ‘값’과 연결한다**고 주장합니다. 에피소드 기억은 사실상 구체적인 ‘에피소드 맥락 키’를 통해 신피질에 축적된 의미적 정보와 결합되어야만 “내용 있는” 기억이 되니까요(예: 의미치매 환자에게서 최근 기억은 살아 있어도, 언어·개념적 이해가 무너지는 경우).

정말 해마가 ‘키’를 제공한다면, 인출 과정에서 **해마가 신피질 활성화를 ‘선행(causal)’**해야 하고, 또 **이 신피질 재활성이 실제 기억 재생에 필수적**이어야 합니다. 실제로, “인출 시 피질의 인코딩 관련 활동이 재활성(reinstatement)되고, 해마가 이를 돕는다”는 뇌 영상·전기생리학적 증거들이 나옵니다(Staresina et al., 2012; Bosch et al., 2014; Tanaka et al., 2014; Danker et al., 2017; Pacheco Estefan et al., 2019; Hebscher et al., 2021).

또 다른 근거는 ‘과잉 일반화’ 현상입니다. 해마가 없으면(또는 기능이 떨어지면) 신피질 값들에 ‘정밀 검색’이 어려워, 에피소드 세부가 뒤섞이기 쉽습니다. Winocur et al.(2009)의 쥐 실험에서, A라는 맥락에서 전기충격 학습을 받은 쥐가, 1일 후에는 A에서만 강하게 얼어붙고 B에선 별로 반응하지 않지만, 1주 후에는 A든 B든 얼어붙는 식으로 맥락 분리가 안 됩니다. 그런데 실험자가 잠깐 A 맥락을 다시 보여주면, 그 에피소드가 구체적으로 다시 떠오르면서 맥락 특이성이 복원되죠. 하지만 해마가 없는 쥐에선 이 복원 효과가 안 나타납니다(Wiltgen et al., 2010).

이는 Teyler와 DiScenna(1986)가 제안한 “해마 기억 인덱싱 이론”과도 맥이 닿습니다. 해마가, 신피질 여기저기에 저장된 정보들을 가리키는 인덱스(키) 역할을 한다는 것. 최근에는 ‘엔그램 세포’를 직접 라벨링·광유전학적으로 조작할 수 있게 되면서, 해마가 진짜로 특정 기억에 연결된 “허브” 노드임이 더욱 부각되었습니다(Liu et al., 2012; Ramirez et al., 2013; Goode et al., 2020).

뇌 전체로 보면 여러 영역이 엔그램 역할을 할 수 있지만, 해마가 고도로 희소한 방식으로(conjunctive tuning) 여러 감각·인지 요소를 묶어내고, 뇌 전역과 강력하게 연결되어 있어 “키”로써 기능하기에 최적화된 것으로 보입니다. 실제로 Chettih et al.(2024)는 저장된 100개 이상의 ‘저장 장소’(혹은 같은 위치의 여러 캐싱) 정보를 해마 세포 집단이 각각 유일하게 인코딩하고, 기억 불러오기 시 이를 재활성한다는 결과를 보였습니다.

**해마 표현이 어떻게 구별성을 최적화**하느냐도 흥미로운데, 예컨대 서로 중복되는 장소·경로를 학습할 때, 해마 뉴런들은 점차 표현을 “반발(repulsion)” 시켜 서로 다른 키를 갖도록 만들어낸다는 연구도 있습니다(Chanales et al., 2017; Wanjia et al., 2021). 이때 반발 정도가 커질수록, 행동적으로도 구분이 더 잘 되었다고 해석됩니다.  
단, 입력 신호가 애매할 때는(잡음·결함이 있을 때는) 키를 보정해(끌개 동력 등으로) 올바른 주소에 도달해야 합니다(패턴 완성). 해마가 CA3·치아이(dentate gyrus)-CA3 루프 등 재귀적 구조를 통해 이를 수행한다는 설도 있습니다(Rolls, 2013; Chandra et al., 2023).

결국 **해마=키, 신피질=값**이라는 분업론은, 매우 미시적인 실험 결과들(해마 신경활동, 엔그램, 반발 표현 등)을 설명하는 데도 부합합니다.

---

#### 4.3 Values, but not keys, are available for recall  
(값은 회상이 되지만, 키 자체는 의식적 회상 대상이 아니다)

키에 저장된 정보는 그대로 의식에 올라오지 않는다고 주장하는 근거는, “인출을 유도하는 단서(키 정보)는 분명히 작동하지만, 정작 그 자체 내용은 우리가 보고하지 못할 때” 발견할 수 있습니다. 예컨대 다음과 같은 현상이 이를 보여줍니다:

- **‘혀끝에서 맴도는 현상(tip-of-the-tongue)’**(Brown and McNeill, 1966; Brown, 1991): 분명 기억이 ‘있다’고 느끼는데, 끝내 내용(값)이 떠오르지 않음.  
- **‘feeling of knowing’**(Hart, 1965): 어떤 문제를 보자마자 “내가 이거 답 알 수 있을 것 같아”라고 예감하지만, 실제 답은 아직 떠오르지 않음.  
- **메타기억(Metamemory) 실험**: 위와 비슷한 현상을 체계적으로 연구했는데, “사실 답을 아직 모르는 상태에서 ‘알 수 있을 것 같은 느낌(키 유사도)’만 보고도, 맞출 가능성이 높은지 아닌지를 예측한다”는 결과가 있습니다. Reder(1987)의 연구에서는 사람들에게 “이 문제는 풀 수 있을까?”를 판단하게 했을 때, 실제 답을 떠올리는 것보다 그 예측 판단이 훨씬 빨랐습니다. 즉, 키 수준에서의 매칭 신호가 별도로 존재할 가능성을 시사합니다.

또한, **짧은 기간 기억(short-term memory)**에서도 “무엇이 변했는지는 모르겠는데, 무언가 바뀐 건 안다”는 식의 변화 감지 현상(Ball and Busch, 2015)도 키-값 분리로 설명 가능합니다(Ruchkin et al., 2003; Norris, 2017). 즉, 키(“변화 감지” 신호)는 올라오지만, 구체적 값(“무엇이 어떻게 바뀌었는가?”)은 불러오지 못하는 상황이지요.

많은 전통적 모델에서는 인출 판단(“알 것 같다”)을 하려면 부분적으로라도 실제 기억 내용을 꺼내야 한다고 봅니다. 하지만 여기서는 키-값 분리가 가능하니, 키 단서만으로도 “기억에 어떤 항목이 있다”고 판정할 수 있고, 값 부분을 굳이 재생하지 않아도 되는 거죠.

---

### **5 Illustrative simulations**  
(모형 시뮬레이션 예시)

이 장에서는, 위에서 강조한 키-값 모델의 특성을 보여주는 두 가지 단순 시뮬레이션을 제시합니다. 자세한 구현은 https://github.com/kazuki-irie/kv-memory-brain 에서 볼 수 있습니다.

---

#### 5.1 Distinct representations for keys and values  
(키와 값을 별도로 표현해 최적화)

키-값 메모리의 핵심은 “키와 값이 각각 다른 목적을 위해 최적화”된다는 겁니다. 여기서는 이를 간단한 예제로 시각화해 봅니다.

2차원(2D) 키, 2D 값 총합 네 개 벡터 쌍을 학습하는 극단적 단순 모델을 만듭니다. 인출 시 질의(쿼리)는 소프트맥스 기반 어텐션(Eq. 5, 6)으로 모든 키와 비교해 가중치를 구하고, 그 가중치로 값들을 가중합해 최종 출력을 냅니다(Eq. 2). 학습 목표는 “(키1)를 질의로 넣었을 때 (값1)를 출력”하도록 만드는 것이며, 각각 ‘클래스’가 2개인 경우와 3개인 경우를 시도합니다.

결과(그림 2)를 보면, **키들은 서로 확실히 구분되는 위치**로 이동해, 질의-키 내적이 쉽게 구별되도록 구조화됩니다. 반면 **값들은 원하는 내용(클래스 특성)을 그대로 담도록 배치**됩니다. 즉, 키·값이 서로 다른 최적화를 따르는 모습을 알 수 있습니다.

---

#### 5.2 Forgetting as retrieval failure, and recovery by memory reactivation  
(망각을 인출 실패로 보고, 기억 재활성으로 복원하기)

다음 예시는 “기억이 실제로 소멸된 것이 아니라 인출 실패”라는 개념과, “침묵된 기억이 재활성으로 되살아나는” 현상을 보여줍니다. 실제 뇌 실험에서 해마에 광유전학 자극을 줘 과거 기억을 다시 떠올리는 실험(Ryan et al., 2015; Roy et al., 2017)과 유사한 맥락입니다.

우리는 두 가지 분류 과제를 순차 학습하는 간단한 신경망(피드포워드 1은닉층)을 만듭니다. 첫 과제(Task 1)는 MNIST 데이터셋의 숫자 0,1만 분류하고, 두 번째 과제(Task 2)는 FashionMNIST 데이터셋의 티셔츠, 바지 이미지를 분류합니다. 모델은 784→64→4 구조이며 ReLU를 거친 뒤 소프트맥스 분류를 사용합니다. 먼저 5 에포크 동안 Task 1을 학습해 정확도 약 99%를 달성하고, 그 뒤 Task 2 데이터로 추가 5 에포크 학습해 약 95% 정확도를 얻습니다.

그 과정에서(그림 3A), Task 2 학습이 시작된 후에는 Task 1 정확도가 9% 수준으로 폭락합니다(‘망각’). 하지만 키-값 시점에서 보면, Task 1 학습 때 생성된 키/값 쌍은 여전히 메모리에 남아 있습니다(경사하강법으로 갱신된 선형층 해석 참고). 다만 “인출 우선순위” 혹은 “검색 매칭”이 뒤덮여 접근이 불가해진 상태라고 볼 수 있습니다.

흥미로운 건, Task 1에 해당하는 키(또는 값)를 인위적으로 확대(스칼라 배수 \(\beta\) 부여)해주는 간단한 조작만으로 Task 1 정확도가 다시 올라간다는 사실입니다(그림 3B). 이는 뇌 과학에서 “광유전학으로 침묵된 해마 엔그램을 재활성하면, 사라진 것 같던 기억이 되살아난다”는 현상과 유사합니다.

결론적으로, 이 실험은 “저장된 기억이 ‘침묵’ 상태로 갈 수 있으나, 적절한 조작(복원)으로 다시 볼 수 있다”는 점을 시사해 줍니다.

---

### **6 Conclusions**  
(결론)

이 논문에서, 우리는 키-값 기억 개념을 인공지능·인지과학·신경과학 전반과 연결 지어 살펴봤습니다. 특히, 해마와 신피질의 분업(키 vs. 값)을 뇌가 실제로 구현하고 있을 가능성을 제시하고, 사람들의 기억 현상(“아는 것 같은데 기억 안 난다”, “침묵된 기억의 복원” 등)이 키-값 구조로 더 쉽게 설명된다는 근거들을 논의했습니다.

물론 이 아이디어들은 아직 가설적입니다. 실험적으로는, 예를 들어 해마 표현에서의 반발 효과가 실제로 가역적(필요에 따라 다시 중첩 가능)인지 등을 더 직접적으로 테스트할 필요가 있습니다. 이론적으로도, 더 정교한 생물학적 모델이 필요합니다.

그럼에도, 트랜스포머나 빠른 가중치 프로그래머 같은 최신 AI 모델에서 키-값 메모리가 핵심이라는 점은 시사하는 바가 큽니다. 뇌 역시 유사한 방식을 활용하고 있다면, 이는 **자연 지능과 인공 지능이 ‘키-값’이라는 공진화적 솔루션**에 수렴하고 있음을 보여주는 예가 될 것입니다(Gershman, 2024).

---

### **Acknowledgments**  
(감사의 말)

저자들은 Kempner Institute for the Study of Natural and Artificial Intelligence와, 미국 국방부(육군연구청 ARO) MURI 프로그램 W911NF-23-1-0277의 지원에 감사를 표합니다.

---

### **Declaration of interests**  
(이해관계 선언)

저자들은 경쟁적 이해관계가 없음을 선언합니다.

---

### **References**  
(참고문헌; 원문에 적힌 순서대로 그대로 번역 없이 표기)

Aizerman, M., Braverman, E., and Rozonoer, L. (1964). Theoretical foundations of the potential  
function method in pattern recognition learning. Automation and Remote Control, 25:821–837.

Allen-Zhu, Z. and Li, Y. (2024). Physics of language models: Part 3.1, knowledge storage and  
extraction. In Forty-first International Conference on Machine Learning.

Amari, S.-I. (1972). Learning patterns and pattern sequences by self-organizing nets of threshold  
elements. IEEE Transactions on Computers, 100:1197–1206.

Amit, D. J., Gutfreund, H., and Sompolinsky, H. (1987). Statistical mechanics of neural networks  
near saturation. Annals of Physics, 173:30–67.

Anderson, J. A. (1970). Two models for memory organization using interacting traces.  
Mathematical Biosciences, 8:137–160.

Ba, J., Hinton, G. E., Mnih, V., Leibo, J. Z., and Ionescu, C. (2016). Using fast weights to attend to  
the recent past. In Advances in Neural Information Processing Systems, pages 4331–4339, Barcelona,  
Spain.

Bahrick, H., Bahrick, P., and Wittlinger, R. (1975). Fifty years of memory for names and faces: A  
cross-sectional approach. Journal of Experimental Psychology: General, 104:54–75.

Bahrick, H. P. and Hall, L. K. (1991). Lifetime maintenance of high school mathematics content.  
Journal of Experimental Psychology: General, 120:20–33.

Ball, F. and Busch, N. A. (2015). Change detection on a hunch: Pre-attentive vision allows “sensing”  
of unique feature changes. Attention, Perception, & Psychophysics, 77:2570–2588.

Barnes, J. M. and Underwood, B. J. (1959). “fate” of first-list associations in transfer theory.  
Journal of experimental psychology, 58:97–105.

Battaglia, F. P., Benchenane, K., Sirota, A., Pennartz, C. M., and Wiener, S. I. (2011). The  
hippocampus: hub of brain network communication for memory. Trends in Cognitive Sciences,  
15(7):310–318.

Bein, O., Plotkin, N. A., and Davachi, L. (2021). Mnemonic prediction errors promote detailed  
memories. Learning & Memory, 28:422–434.

Berens, S. C., Richards, B. A., and Horner, A. J. (2020). Dissociating memory accessibility and  
precision in forgetting. Nature Human Behaviour, 4:866–877.

Bittner, K. C., Milstein, A. D., Grienberger, C., Romani, S., and Magee, J. C. (2017). Behavioral  
time scale synaptic plasticity underlies ca1 place fields. Science, 357:1033–1036.

Bosch, S. E., Jehee, J. F., Fernández, G., and Doeller, C. F. (2014). Reinstatement of associative  
memories in early visual cortex is signaled by the hippocampus. Journal of Neuroscience,  
34:7493–7500.

Bradley, P. and Galal, K. (1988). State-dependent recall can be induced by protein synthesis  
inhibition: behavioural and morphological observations. Developmental Brain Research,  
40:243–251.

Bricken, T., Davies, X., Singh, D., Krotov, D., and Kreiman, G. (2023). Sparse distributed memory  
is a continual learner. In International Conference on Learning Representations.

Briggs, J. F. and Olson, B. P. (2013). Reexposure to the amnestic agent alleviates cycloheximide-  
induced retrograde amnesia for reactivated and extinction memories. Learning & Memory, 20:285–288.

Brown, A. (1991). A review of the tip-of-the-tongue experience. Psychological Bulletin, 109:204–223.

Brown, R. and McNeill, D. (1966). The “tip of the tongue” phenomenon. Journal of Verbal Learning  
and Verbal Behavior, 5:325–337.

Buschke, H. (1974). Spontaneous remembering after recall failure. Science, 184:579–581.

Caporale, N. and Dan, Y. (2008). Spike timing-dependent plasticity: A hebbian learning rule.  
Annual Review of Neuroscience, 31:25–46.

Chandra, S., Sharma, S., Chaudhuri, R., and Fiete, I. (2023). High-capacity flexible hippocampal  
associative and episodic memory enabled by prestructured “spatial” representations. bioRxiv,  
pages 2023–11.

Chanales, A. J., Oza, A., Favila, S. E., and Kuhl, B. A. (2017). Overlap among spatial memories  
triggers repulsion of hippocampal representations. Current Biology, 27:2307–2317.

Chaudhuri, R. and Fiete, I. (2016). Computational principles of memory. Nature Neuroscience,  
19:394–403.

Chettih, S. N., Mackevicius, E. L., Hale, S., and Aronov, D. (2024). Barcoding of episodic memories  
in the hippocampus of a food-caching bird. Cell, 187:1922–1935.

Choromanski, K. M., Likhosherstov, V., Dohan, D., Song, X., Gane, A., Sarlos, T., Hawkins, P.,  
Davis, J. Q., Mohiuddin, A., Kaiser, L., Belanger, D. B., Colwell, L. J., and Weller, A. (2021).  
Rethinking attention with performers. In International Conference on Learning Representations.

Conway, M. A., Cohen, G., and Stanhope, N. (1991). On the very long-term retention of knowledge  
acquired through formal education: Twelve years of cognitive psychology. Journal of Experimental  
Psychology: General, 120:395–409.

Crowder, R. G. (1976). Principles of Learning and Memory. Lawrence Erlbaum.

Danker, J. F., Tompary, A., and Davachi, L. (2017). Trial-by-trial hippocampal encoding activation  
predicts the fidelity of cortical reinstatement during subsequent retrieval. Cerebral Cortex,  
27:3515–3524.

Diamond, N. B., Armson, M. J., and Levine, B. (2020). The truth is out there: Accuracy in recall of  
verifiable real-world events. Psychological Science, 31:1544–1556.

Dudai, Y. (1997). How big is human memory, or on being just useful enough. Learning & Memory,  
3:341–365.

Estes, W. (1955). Statistical theory of spontaneous recovery and regression. Psychological Review,  
62:145–154.

Flexner, L., Flexner, J., and Roberts, R. (1966). Stages of memory in mice treated with acetoxy-  
cycloheximide before or immediately after learning. Proceedings of the National Academy of  
Sciences, 56:730–735.

Freedman, J. and Landauer, T. (1966). Retrieval of long-term memory: “tip-of-the-tongue”  
phenomenon. Psychonomic Science, 4:309–310.

French, R. M. (1999). Catastrophic forgetting in connectionist networks. Trends in cognitive  
sciences, 3(4):128–135.

Gershman, S. J. (2024). What have we learned about artificial intelligence from studying the brain?  
Biological Cybernetics, pages 1–5.

Gershman, S. J. and Daw, N. D. (2017). Reinforcement learning and episodic memory in humans  
and animals: an integrative framework. Annual Review of Psychology, 68:101–128.

Geva, M., Schuster, R., Berant, J., and Levy, O. (2021). Transformer feed-forward layers are key-  
value memories. In Proceedings of the 2021 Conference on Empirical Methods in Natural Language  
Processing, pages 5484–5495.

Gisquet-Verrier, P., Lynch, J. F., Cutolo, P., Toledano, D., Ulmen, A., Jasnow, A. M., and Riccio, D. C.  
(2015). Integration of new information with active memory accounts for retrograde amnesia: a  
challenge to the consolidation/reconsolidation hypothesis? Journal of Neuroscience, 35:11623–11633.

Goode, T. D., Tanaka, K. Z., Sahay, A., and McHugh, T. J. (2020). An integrated index: engrams,  
place cells, and hippocampal memory. Neuron, 107:805–820.

Graham, K. S., Patterson, K., and Hodges, J. R. (1999). Episodic memory: new insights from the  
study of semantic dementia. Current Opinion in Neurobiology, 9:245–250.

Graves, A., Wayne, G., Reynolds, M., Harley, T., Danihelka, I., Grabska-Barwinska, A.,  
Colmenarejo, S. G., Grefenstette, E., Ramalho, T., Agapiou, J., et al. (2016). Hybrid computing  
using a neural network with dynamic external memory. Nature, 538:471–476.

Green, R. (1956). Surprise as a factor in the von Restorff effect. Journal of Experimental Psychology,  
52:340–344.

Gruneberg, M. M. and Monks, J. (1974). ‘feeling of knowing’ and cued recall. Acta Psychologica,  
38:257–265.

Hafting, T., Fyhn, M., Molden, S., Moser, M.-B., and Moser, E. I. (2005). Microstructure of a spatial  
map in the entorhinal cortex. Nature, 436:801–806.

Hart, J. (1965). Memory and the feeling-of-knowing experience. Journal of Educational Psychology,  
56:208–216.

Hebscher, M., Kragel, J. E., Kahnt, T., and Voss, J. L. (2021). Enhanced reinstatement of  
naturalistic event memories due to hippocampal-network-targeted stimulation. Current Biology,  
31:1428–1437.

Hirshman, E., Whelley, M. M., and Palij, M. (1989). An investigation of paradoxical memory effects.  
Journal of Memory and Language, 28:594–609.

Hopfield, J. J. (1982). Neural networks and physical systems with emergent collective computational  
abilities. Proceedings of the National Academy of Sciences, 79:2554–2558.

Irie, K., Csordás, R., and Schmidhuber, J. (2022). The dual form of neural networks revisited:  
Connecting test time predictions to training patterns via spotlights of attention. In International  
Conference on Machine Learning, pages 9639–9659. PMLR.

Kahana, M. J. (2012). Foundations of Human Memory. Oxford University Press.

Kanerva, P. (1988). Sparse Distributed Memory. MIT Press.

Kapur, N. (1999). Syndromes of retrograde amnesia: a conceptual and empirical synthesis.  
Psychological Bulletin, 125:800–825.

Katharopoulos, A., Vyas, A., Pappas, N., and Fleuret, F. (2020). Transformers are RNNs: Fast  
autoregressive transformers with linear attention. In Proceedings of the 37th International  
Conference on Machine Learning, volume 119 of Proceedings of Machine Learning Research, pages  
5156–5165. PMLR.

Kohonen, T. (1972). Correlation matrix memories. IEEE transactions on computers, 100:353–359.

Kohonen, T. (1980). Content-Addressable Memories. Springer Science & Business Media.

Koriat, A. and Lieblich, I. (1977). A study of memory pointers. Acta Psychologica, 41:151–164.

Kozachkov, L., Kastanenka, K. V., and Krotov, D. (2023). Building transformers from neurons and  
astrocytes. Proceedings of the National Academy of Sciences, 120:e2219150120.

Krotov, D. and Hopfield, J. J. (2016). Dense associative memory for pattern recognition. In Advances  
in Neural Information Processing Systems, volume 29.

Kumaran, D., Hassabis, D., and McClelland, J. L. (2016). What learning systems do intelligent  
agents need? complementary learning systems theory updated. Trends in Cognitive Sciences,  
20:512–534.

Landauer, T. K. (1975). Memory without organization: Properties of a model with random storage  
and undirected retrieval. Cognitive Psychology, 7:495–531.

LeCun, Y., Cortes, C., and Burges, C. J. (1998). The MNIST database of handwritten digits. URL  
http://yann.lecun.com/exdb/mnist.

Lewis, D. J. (1979). Psychobiology of active and inactive memory. Psychological bulletin, 86(5):1054.

Lewis, D. J., Misanin, J. R., and Miller, R. R. (1968). Recovery of memory following amnesia. Nature,  
220(5168):704–705.

Lillicrap, T. P., Santoro, A., Marris, L., Akerman, C. J., and Hinton, G. (2020). Backpropagation and  
the brain. Nature Reviews Neuroscience, 21:335–346.

Limbacher, T. and Legenstein, R. (2020). H-mem: Harnessing synaptic plasticity with hebbian  
memory networks. Advances in Neural Information Processing Systems, 33:21627–21637.

Liu, X., Ramirez, S., Pang, P. T., Puryear, C. B., Govindarajan, A., Deisseroth, K., and Tonegawa, S.  
(2012). Optogenetic stimulation of a hippocampal engram activates fear memory recall. Nature,  
484:381–385.

Mandler, G. (1980). Recognizing: The judgment of previous occurrence. Psychological Review,  
87:252–271.

Maxcey, A. M., Shiffrin, R. M., Cousineau, D., and Atkinson, R. C. (2021). Two case studies of very  
long-term retention. Psychonomic Bulletin & Review, pages 1–5.

McClelland, J., McNaughton, B., and O’Reilly, R. (1995). Why there are complementary learning  
systems in the hippocampus and neocortex: insights from the successes and failures of  
connectionist models of learning and memory. Psychological Review, 102:419–457.

McCloskey, M. and Cohen, N. J. (1989). Catastrophic interference in connectionist networks: The  
sequential learning problem. In Psychology of Learning and Motivation, volume 24, pages 109–165.  
Elsevier.

Miller, A., Fisch, A., Dodge, J., Karimi, A.-H., Bordes, A., and Weston, J. (2016). Key-value memory  
networks for directly reading documents. In Proceedings of the 2016 Conference on Empirical Methods  
in Natural Language Processing, pages 1400–1409.

Miller, R. R. (2021). Failures of memory and the fate of forgotten memories. Neurobiology of  
Learning and Memory, 181:107426.

Millidge, B., Salvatori, T., Song, Y., Lukasiewicz, T., and Bogacz, R. (2022). Universal Hopfield  
networks: A general framework for single-shot associative memory models. In International  
Conference on Machine Learning, pages 15561–15583. PMLR.

Morton, J., Hammersley, R. H., and Bekerian, D. (1985). Headed records: A model for memory  
and its failures. Cognition, 20:1–23.

Nakano, K. (1972). Associatron–a model of associative memory. IEEE Transactions on Systems,  
Man, and Cybernetics, pages 380–388.

Norris, D. (2017). Short-term memory and long-term memory are still different. Psychological  
Bulletin, 143:992–1009.

O’Reilly, R. C. and Norman, K. A. (2002). Hippocampal and neocortical contributions to memory:  
Advances in the complementary learning systems framework. Trends in Cognitive Sciences,  
6(12):505–510.

Pacheco Estefan, D., Sánchez-Fibla, M., Duff, A., Principe, A., Rocamora, R., Zhang, H., Axmacher, N.,  
and Verschure, P. F. (2019). Coordinated representational reinstatement in the human hippocam  
pus and lateral temporal cortex during episodic memory retrieval. Nature Communications,  
10:2255.

Pavlov, I. (1927). Conditioned Reflexes. Oxford University Press.

Payne, D. (1987). Hypermnesia and reminiscence in recall: a historical and empirical review.  
Psychological Bulletin, 101:5–27.

Peng, H., Pappas, N., Yogatama, D., Schwartz, R., Smith, N. A., and Kong, L. (2021). Random  
feature attention. In International Conference on Learning Representations.

Pike, R. (1984). Comparison of convolution and matrix distributed memory systems for associative  
recall and recognition. Psychological Review, 91:281–294.

Radhakrishnan, A., Belkin, M., and Uhler, C. (2020). Overparameterized neural networks  
implement associative memory. Proceedings of the National Academy of Sciences, 117:27162–27170.

Ramirez, S., Liu, X., Lin, P.-A., Suh, J., Pignatelli, M., Redondo, R. L., Ryan, T. J., and Tonegawa, S.  
(2013). Creating a false memory in the hippocampus. Science, 341:387–391.

Ramsauer, H., Schäfl, B., Lehner, J., Seidl, P., Widrich, M., Gruber, L., Holzleitner, M., Adler, T.,  
Kreil, D., Kopp, M. K., Klambauer, G., Brandstetter, J., and Hochreiter, S. (2021). Hopfield  
networks is all you need. In International Conference on Learning Representations.

Ratcliff, R. (1990). Connectionist models of recognition memory: constraints imposed by learning  
and forgetting functions. Psychological review, 97(2):285.

Reder, L. M. (1987). Strategy selection in question answering. Cognitive Psychology, 19:90–138.

Reder, L. M. and Ritter, F. E. (1992). What determines initial feeling of knowing? familiarity with  
question terms, not with the answer. Journal of Experimental Psychology: Learning, Memory, and  
Cognition, 18:435–451.

Rescorla, R. and Heth, C. (1975). Reinstatement of fear to an extinguished conditioned stimulus.  
Journal of Experimental psychology. Animal Behavior Processes, 1:88–96.

Riccio, D. C. and Richardson, R. (1984). The status of memory following experimentally induced  
amnesias: Gone, but not forgotten. Physiological Psychology, 12:59–72.

Roediger, H. and Thorpe, L. (1978). The role of recall time in producing hypermnesia. Memory &  
Cognition, 6:296–305.

Rolls, E. T. (2013). The mechanisms for pattern completion and pattern separation in the hippo  
campus. Frontiers in Systems Neuroscience, 7:74.

Rouhani, N., Norman, K., and Niv, Y. (2018). Dissociable effects of surprising rewards on learning  
and memory. Journal of Experimental psychology. Learning, Memory, and Cognition, 44:1430–1443.

Roy, D. S., Muralidhar, S., Smith, L. M., and Tonegawa, S. (2017). Silent memory engrams as the  
basis for retrograde amnesia. Proceedings of the National Academy of Sciences, 114(46):E9972–E9979.

Roy, D. S., Park, Y.-G., Kim, M. E., Zhang, Y., Ogawa, S. K., DiNapoli, N., Gu, X., Cho, J. H., Choi,  
H., Kamentsky, L., et al. (2022). Brain-wide mapping reveals that engrams for a single memory  
are distributed across multiple brain regions. Nature Communications, 13:1799.

Ruchkin, D. S., Grafman, J., Cameron, K., and Berndt, R. S. (2003). Working memory retention  
systems: A state of activated long-term memory. Behavioral and Brain sciences, 26:709–728.

Ryan, T. J., Roy, D. S., Pignatelli, M., Arons, A., and Tonegawa, S. (2015). Engram cells retain  
memory under retrograde amnesia. Science, 348(6238):1007–1013.

Sakamoto, Y. and Love, B. C. (2004). Schematic influences on category learning and recognition  
memory. Journal of Experimental Psychology: General, 133:534–553.

Schlag, I., Irie, K., and Schmidhuber, J. (2021). Linear transformers are secretly fast weight pro  
grammers. In Proceedings of the 38th International Conference on Machine Learning, volume 139 of  
Proceedings of Machine Learning Research, pages 9355–9366. PMLR.

Schmidhuber, J. (1992). Learning to control fast-weight memories: An alternative to dynamic  
recurrent networks. Neural Computation, 4(1):131–139.

Schölkopf, B. (2002). Learning with Kernels: Support Vector Machines, Regularization, Optimization,  
and Beyond. MIT Press.

Schwartz, B. and Metcalfe, J. (1992). Cue familiarity but not target retrievability enhances feeling-  
of-knowing judgments. Journal of Experimental psychology. Learning, Memory, and Cognition,  
18:1074–1083.

Serota, R. G. (1971). Acetoxycycloheximide and transient amnesia in the rat. Proceedings of the  
National Academy of Sciences, 68:1249–1250.

Sharma, S., Chandra, S., and Fiete, I. (2022). Content addressable memory without catastrophic  
forgetting by heteroassociation with a fixed scaffold. In International Conference on Machine  
Learning, pages 19658–19682. PMLR.

Shiffrin, R. M. (1970). Forgetting: Trace erosion or retrieval failure? Science, 168:1601–1603.

Squire, L. R. and Barondes, S. H. (1972). Variable decay of memory and its recovery in cyclo-  
heximide-treated mice. Proceedings of the National Academy of Sciences, 69:1416–1420.

Staresina, B. P., Henson, R. N., Kriegeskorte, N., and Alink, A. (2012). Episodic reinstatement in  
the medial temporal lobe. Journal of Neuroscience, 32:18150–18156.

Steinbuch, K. and Piske, U. A. W. (1963). Learning matrices and their applications. IEEE  
Transactions on Electronic Computers, 12(6):846–862.

Sukhbaatar, S., Szlam, A., Weston, J., and Fergus, R. (2015). End-to-end memory networks. In  
Advances in Neural Information Processing Systems, volume 28. Curran Associates, Inc.

Tanaka, K. Z., Pevzner, A., Hamidi, A. B., Nakazawa, Y., Graham, J., and Wiltgen, B. J. (2014).  
Cortical representations are reinstated by the hippocampus during memory retrieval. Neuron,  
84:347–354.

Teyler, T. and DiScenna, P. (1986). The hippocampal memory indexing theory. Behavioral  
Neuroscience, 100:147–154.

Teyler, T. J. and Rudy, J. W. (2007). The hippocampal indexing theory and episodic memory:  
updating the index. Hippocampus, 17:1158–1169.

Tsai, Y.-H. H., Bai, S., Yamada, M., Morency, L.-P., and Salakhutdinov, R. (2019). Transformer  
dissection: An unified understanding for transformer’s attention via the lens of kernel. In  
Proceedings of the Conference on Empirical Methods in Natural Language Processing and the 9th  
International Joint Conference on Natural Language Processing (EMNLP-IJCNLP), pages 4344–4353,  
Hong Kong, China. Association for Computational Linguistics.

Tulving, E. (1974). Cue-dependent forgetting. American Scientist, 62:74–82.

Tyulmankov, D., Fang, C., Vadaparty, A., and Yang, G. R. (2021). Biological learning in key-value  
memory networks. Advances in Neural Information Processing Systems, 34:22247–22258.

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, L. u., and  
Polosukhin, I. (2017). Attention is all you need. In Advances in Neural Information Processing  
Systems, volume 30.

Vetere, G., Kenney, J. W., Tran, L. M., Xia, F., Steadman, P. E., Parkinson, J., Josselyn, S. A., and  
Frankland, P. W. (2017). Chemogenetic interrogation of a brain-wide fear memory network in  
mice. Neuron, 94:363–374.

Wagenaar, W. A. (1986). My memory: A study of autobiographical memory over six years.  
Cognitive Psychology, 18:225–252.

Wanjia, G., Favila, S. E., Kim, G., Molitor, R. J., and Kuhl, B. A. (2021). Abrupt hippocampal  
remapping signals resolution of memory interference. Nature Communications, 12:4816.

Willshaw, D. J., Buneman, O. P., and Longuet-Higgins, H. C. (1969). Non-holographic associative  
memory. Nature, 222(5197):960–962.

Wiltgen, B. J., Zhou, M., Cai, Y., Balaji, J., Karlsson, M. G., Parivash, S. N., Li, W., and Silva, A. J.  
(2010). The hippocampus plays a selective role in the retrieval of detailed contextual memories.  
Current Biology, 20:1336–1344.

Winocur, G., Frankland, P. W., Sekeres, M., Fogel, S., and Moscovitch, M. (2009). Changes in  
context-specificity during memory reconsolidation: selective effects of hippocampal lesions.  
Learning & Memory, 16:722–729.

Xiao, H., Rasul, K., and Vollgraf, R. (2017). Fashion-MNIST: a novel image dataset for  
benchmarking machine learning algorithms. Preprint arXiv:1708.07747.
