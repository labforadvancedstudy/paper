Memory Layers at Scale (2024.12)
- Vincent-Pierre Berges, Barlas Oğuz, Daniel Haziza, Wen-tau Yih, Luke Zettlemoyer, Gargi Ghosh
- https://arxiv.org/abs/2412.09764

---

## 요약·설명

이 논문은 거대 언어모델(LLM) 아키텍처에서 **"Memory Layer"** 라고 불리는 구조를 활용하여, 추가적인 파라미터(메모리)를 늘리면서도 계산 복잡도(FLOPs)를 크게 증가시키지 않고 모델의 성능을 높이는 연구를 다룬 거야. 간단히 말해, 전통적인 ‘밀집(dense) 피드포워드 레이어’를 모두 사용하는 대신, 일부 레이어를 “메모리 레이어”로 교체해서 **값(key-value) 조회** 형태로 필요한 정보를 효율적으로 불러와 활용하겠다는 아이디어야.

### 핵심 개념
- **Memory Layers**: 
  - 키/값(key-value) 형태로 정보를 저장하고, 입력 쿼리(query)와 유사도가 높은 키를 골라, 해당하는 값만 가져와 연산에 활용하는 구조.
  - 파라미터(메모리)는 많아지지만, 실제로 매번 활성화되는 메모리(=연산)는 소량(top-k)만 쓰이므로 FLOPs가 크게 증가하지 않음.
  - 완전히 밀집된(dense) FFN 레이어와 달리, **희소(sparse)한 접근**을 통해 대규모 지식·정보를 파라미터로 저장하고 필요 시 빠르게 꺼내 쓸 수 있음.

- **연구 동기**: 
  - 현재 대형 모델(예: GPT, Llama 등)은 파라미터가 커지면 커질수록 학습 및 추론에 필요한 **계산량이 기하급수적으로 증가**함.
  - 그런데, 모든 ‘사실 정보’나 ‘단순 연관관계’를 밀집 파라미터에 담아두는 것이 최선일까?  
  - (연구팀 주장) “단순히 외부 지식을 많이 외우는 영역은, **매트릭스乘 연산보다 키-값 조회**가 더 적합할 수 있다.”
  - MOE(Mixture-of-Experts)와 유사하게 ‘파라미터는 크게, 계산은 선택적으로’ 하는 접근이지만, MOE와 다르게 **메모리 형태**로 좀 더 효율적으로 설계.

- **주요 실험**:
  - 다양한 크기의 베이스 모델(134M ~ 8B 파라미터)에 대해 **일부 레이어를 메모리 레이어로 교체**하고, 이를 크게(최대 128B 파라미터)까지 확장해봄.
  - 결과적으로, **메모리 레이어를 도입한 모델**이 (1) 동일하거나 더 적은 FLOPs로도, (2) 훨씬 더 큰 밀집 모델 수준의 성능, 혹은 그 이상의 성능을 낸다는 점을 확인.
  - 특히 사실(knowledge) 관련 QA, 코딩 테스트, 일반 지식 등에 효과가 두드러짐.

- **구현 상세/최적화**: 
  1. **Product-key lookup**으로 키-값 검색 효율을 향상.  
  2. **병렬화(parallelization)** 기법으로 대규모 메모리(수백만~수억개의 키/값)도 GPU 여러 대에 나눠서 처리.  
  3. **Shared memory**: 여러 개의 메모리 레이어가 하나의 거대한 키-값 풀을 공유하도록 설계해, 파라미터 효율↑.  
  4. **커스텀 CUDA 커널**(EmbeddingBag 등)을 직접 최적화해서 PyTorch 기본보다 훨씬 빠른 메모리 접근 구현.  
  5. **불안정성 개선**: 게이팅(gating), silu 같은 비선형성, kq-normalization 등으로 학습 안정화.

- **결론**:
  - “다음 세대 AI 아키텍처엔 메모리 레이어가 꼭 들어가야 한다”고 강하게 주장.
  - 사실성·지식 저장 관점에서 전통적인 밀집 레이어 대비 훨씬 적은 계산량으로 더 많은 정보를 저장·활용 가능.
  - 아직 산업적 대규모 프로덕션 사용을 위해서는 최적화 과제가 남아있지만, 잠재력이 매우 높다.

---

## 2. 기존 연구 결과까지 고려한 핵심·본질

1. **‘밀집 파라미터’만으로 커버하기엔 비효율이 큰 영역(단순 정보·연관관계)은, ‘희소·키값 메모리’가 더 적합**하다는 것.  
   - 기존에 MOE, Retrieval-Augmented Generation 등도 “모든 파라미터를 동시에 안 쓰고, 필요할 때만 활용”하는 시도를 해왔잖아.  
   - 이 논문은 그 “메모리” 관점에서 더 직접적이고 구조화된 키-값 테이블을 도입해, 단순 매트릭스乘보다 정보를 저장·검색하는 데 효율을 높였어.

2. **실제 규모의 LLM에 도입해 ‘2배 이상 큰 밀집 모델’과 맞먹거나 능가하는 결과**를 보여준다는 점이 중요.  
   - 흔히 “파라미터를 늘리면 당연히 계산비용이 따라 커진다”는 식의 딜레마가 있는데, **메모리 레이어는 파라미터 증가와 계산량 증가의 ‘분리’를 어느 정도 실현**한 사례.

3. **‘사실 관련 QA, 코딩, 지식 테스트’에서 크게 향상** → 결국 메모리 구조가 ‘팩트(사실)’를 저장하기에 적합.  
   - LLM이 “특정 인물의 생일”처럼 단순한 연관관계를 사실적으로 잘 꺼내 쓸 수 있게 도와주어, **“환각(Hallucination)”을 줄이는 데 기여**할 가능성도 시사.

4. **엔지니어링·하드웨어 최적화가 관건**  
   - 장치 메모리 대역폭, CUDA 커널, 분산 병렬 처리 등 다양한 요소를 건드려야 한다.  
   - 지금도 성능을 크게 끌어올리는 잠재력이 있고, 충분히 연구할 가치가 있다는 메시지.

결국 **이 연구의 본질은, 대규모 언어모델의 파라미터 증가=계산량 증가라는 방정식을 깨고**, 희소 메모리 구조를 통해 지식 저장 효율을 크게 높이는 설계 가능성을 보여준 것이라고 볼 수 있어.

---


```
MemoryLayersatScale
 Vincent-Pierre Berges∗, BarlasOğuz∗, DanielHaziza, Wen-tauYih, LukeZettlemoyer, GargiGhosh
 Meta FAIR
 ∗Main authors
```

**번역**:  
**“MemoryLayersatScale”**  
Vincent-Pierre Berges∗, Barlas Oğuz∗, Daniel Haziza, Wen-tau Yih, Luke Zettlemoyer, Gargi Ghosh  
Meta FAIR  
∗주요 저자(Main authors)

```
Memory layers use a trainable key-value lookup mechanism to add extra parameters to a model without
increasing FLOPs. Conceptually, sparsely activated memory layers complement compute-heavy dense
feed-forward layers, providing dedicated capacity to store and retrieve information cheaply. This
work takes memory layers beyond proof-of-concept, proving their utility at contemporary scale.
```
**번역**:  
메모리 레이어는, FLOPs를 늘리지 않고도 모델에 추가 파라미터를 더하기 위해 학습 가능한 키-값 조회 메커니즘을 사용한다. 개념적으로, 희소적으로 활성화되는 메모리 레이어는 계산량이 큰 밀집 피드포워드 레이어를 보완하며, 저렴하게 정보를 저장·검색할 수 있는 전용 용량을 제공한다. 본 연구는 메모리 레이어를 단순 개념 검증 수준을 넘어서, 현대적 규모에서의 유용성을 증명한다.

```
On downstream tasks, language models augmented with our improved memory layer outperform dense
models with more than twice the computation budget, as well as mixture-of-expert models when
matched for both compute and parameters. We find gains are especially pronounced for factual tasks.
```
**번역**:  
다운스트림 과제에서, 우리가 개선한 메모리 레이어로 보강된 언어 모델은, 두 배 이상의 계산 예산을 사용하는 밀집 모델뿐만 아니라, 계산량과 파라미터를 동일하게 맞춘 Mixture-of-Expert 모델도 능가한다. 우리는 이러한 향상이 특히 ‘사실’과 관련된 과제에서 두드러짐을 발견했다.

```
We provide a fully parallelizable memory layer implementation, demonstrating scaling laws with up to
128B memory parameters, pretrained to 1 trillion tokens, comparing to base models with up to 8B
parameters.
```
**번역**:  
우리는 완전히 병렬화 가능한 메모리 레이어 구현을 제공하며, 최대 1280억(128B) 메모리 파라미터까지 확장하여 1조(1T) 토큰에 대해 사전학습한 뒤, 최대 80억(8B) 파라미터를 가진 베이스 모델과 비교하는 스케일링 법칙을 시연한다.

```
Date: December 23, 2024
Correspondence: Vincent-Pierre Berges at vincentpierre@meta.com, Barlas Oğuz at barlaso@meta.com
Code: https://github.com/facebookresearch/memory
Blogpost: https://ai.meta.com/blog/meta-fair-updates-agents-robustness-safety-architecture
```
**번역**:  
날짜: 2024년 12월 23일  
문의: Vincent-Pierre Berges (vincentpierre@meta.com), Barlas Oğuz (barlaso@meta.com)  
코드: <https://github.com/facebookresearch/memory>  
블로그 글: <https://ai.meta.com/blog/meta-fair-updates-agents-robustness-safety-architecture>

---

### 1 Introduction

```
Factual QA Accuracy vs. Memory Size
 60
 NQ
 TQA
 Accuracy
 40
 20
 0
 NLL vs. Memory Size
 Negative Log Likelihood
 12
 10
 NQ
 4 
6 
8
 0
 10242 20482 40962 81922
 Memory Parameters (×2048)
 TQA
 0
 10242 20482 40962 81922
 Memory Parameters (×2048)
```
**번역(그래프 설명)**:  
- 왼쪽: 메모리 크기에 따른 팩추얼 QA 정확도(NQ: NaturalQuestions, TQA: TriviaQA)  
- 오른쪽: 메모리 크기에 따른 NLL(음의 로그가능도). (낮을수록 좋음)  
- 그래프의 파라미터 축: `Memory Parameters (×2048)`  
- 숫자 예: 10242, 20482, 40962, 81922 등은 실제 메모리 파라미터 갯수를 나타내며, ‘×2048’을 곱해 읽음.

```
Figure 1 Scaling the size of the memory for a 1.3 billion parameter base model (zero memory parameters corresponds
to a dense model), trained to 1 trillion tokens. On the left, factual QA accuracy (exact match on NaturalQuestions
and F1 score on TriviaQA), on the right task NLL (lower is better). Dashed lines show the performance of a 7B model
trained on 2 trillion tokens with 10x more FLOPs.
```
**번역**:  
그림 1: 13억(1.3B) 파라미터의 베이스 모델에 대해 메모리 크기를 확장한 결과(메모리 파라미터가 0이면 밀집 모델에 해당)를, 1조(1T) 토큰으로 학습한 경우. 왼쪽은 사실형 QA 정확도(NaturalQuestions는 exact match, TriviaQA는 F1 점수), 오른쪽은 작업별 NLL(낮을수록 좋음). 점선은 2조(2T) 토큰, 10배 더 많은 FLOPs로 학습된 70억(7B) 모델의 성능을 나타낸다.

```
Pretrained language models encode vast amounts of information in their parameters (Roberts et al., 2020),
and they can recall and use this information more accurately with increasing scale (Brown et al., 2020).
For dense deep neural networks, which encode information primarily as weights of linear matrix transforms,
this scaling of parameter size is directly coupled to an increase in computational and energy requirements.
```
**번역**:  
사전학습된 언어 모델은 파라미터에 방대한 양의 정보를 인코딩하며(Roberts et al., 2020), 규모가 커질수록 이 정보를 더 정확히 회상하고 활용할 수 있다(Brown et al., 2020). 그러나 주로 선형 행렬 변환의 가중치 형태로 정보를 인코딩하는 밀집 신경망의 경우, 파라미터 크기를 키우는 것은 계산 및 에너지 요구사항의 증가와 직접적으로 연결된다.

```
It is unclear if this is the most efficient solution to all information storage needs of language models. An
important subset of information that language models need to learn are simple associations. For example,
LLMs learn birthdays of celebrities, capital cities of countries, or how one concept might relate to another.
While feed-forward networks can in principle (given sufficient scale) learn any function (Hornik et al., 1989),
including lookup tables of associations, using an associative memory for this purpose would be both more
efficient and more natural.
```
**번역**:  
이는 언어 모델이 필요로 하는 모든 정보 저장 요구 사항에 대해 최적의 해결책인지 명확하지 않다. 언어 모델이 학습해야 하는 정보 중 중요한 부분은 단순 연관관계로, 예를 들어 유명 인물의 생일, 국가의 수도, 또는 한 개념이 다른 개념과 어떻게 연결되는지 등을 포함한다. 피드포워드 네트워크가 이론적으로(충분한 규모가 주어지면) 이러한 연관관계의 룩업 테이블을 포함해 어떤 함수든 학습 가능하다(Hornik et al., 1989)고 해도, 이러한 용도에 연관 기억(associative memory)을 활용하는 편이 더 효율적이고 자연스러울 것이다.

```
Such memory layers can be implemented with a simple and cheap key-value lookup mechanism where both
keys and values are encoded as embeddings (Weston et al., 2015). Earlier works introduced end-to-end
trainable memory layers (Sukhbaatar et al., 2015) and incorporated them as part of neural computational
systems (Graves et al., 2014). Despite early enthusiasm however, memory layers have not been studied and
scaled sufficiently to be useful in modern AI architectures.
```
**번역**:  
이러한 메모리 레이어는, 키와 값을 임베딩으로 인코딩하는 간단하고 저렴한 키-값 조회 메커니즘을 통해 구현할 수 있다(Weston et al., 2015). 이전 연구에서는 엔드-투-엔드 학습이 가능한 메모리 레이어(Sukhbaatar et al., 2015)를 제안하고, 이를 신경망 연산 시스템의 일부로 통합하기도 했다(Graves et al., 2014). 그러나 초기의 관심에도 불구하고, 메모리 레이어는 현대 AI 아키텍처에서 활용될 만큼 충분히 연구·확장되지 못했다.

```
There are distinctive challenges one encounters when attempting to scale memory layers, which we touch
upon in section 3. In contrast to dense layers which are predominantly FLOP-bound, memory layers with
their sparse activation pattern are almost entirely memory bandwidth bound. Such components are rarely
used in modern architectures and have not been optimised for hardware accelerators. In addition to, and
partly as a result of this, little research was done to improve their performance. Instead, the field focused on
alternatives such as mixture-of-experts (Shazeer et al., 2017), which more closely resemble dense networks
and are thus easier to scale.
```
**번역**:  
메모리 레이어를 대규모로 확장하려 할 때 직면하는 독특한 과제가 있는데, 이에 대해서는 3장에서 다룬다. 주로 FLOP에 의존하는 밀집 레이어와 달리, 희소 활성화 패턴을 가진 메모리 레이어는 거의 전적으로 메모리 대역폭에 의해 제한된다. 이러한 부품은 현대적 아키텍처에서는 드물게 사용되며, 하드웨어 가속기에 최적화되어 있지 않다. 이로 인해, 그리고 일부는 그 결과로, 메모리 레이어의 성능을 개선하기 위한 연구가 거의 이뤄지지 못했다. 대신, 기존 연구 분야는 (Shazeer et al., 2017)에서 제안된 Mixture-of-Experts와 같은 대안을 주로 연구했는데, 이는 밀집 네트워크와 좀 더 유사하여 확장이 용이하기 때문이다.

```
In this work, we show that memory layers, when improved and scaled sufficiently, can be used to augment
dense neural networks to great benefit. We do so by replacing the feed-forward network (FFN) of one or more
transformer layers with memory layers (we leave other layers unchanged). These benefits are consistent across
a range of base model sizes (ranging from 134 million to 8 billion parameters), and memory capacities (up
to 128 billion parameters). This represents a two orders of magnitude leap in memory capacity compared
to previous memory layers reported in the literature.
```
**번역**:  
본 연구에서, 우리는 메모리 레이어가 충분히 개선되고 확장된다면 밀집 신경망을 보강하는 데 큰 이점을 제공할 수 있음을 보인다. 이를 위해 하나 이상의 트랜스포머 레이어에서 피드포워드 네트워크(FFN)를 메모리 레이어로 교체하고, 다른 레이어는 변경하지 않는다. 이러한 이점은 1억 3400만~80억 파라미터에 이르는 다양한 베이스 모델 규모와, 최대 1,280억 파라미터에 이르는 메모리 용량 전반에 걸쳐 일관되게 나타난다. 이는 이전 문헌에 보고된 메모리 레이어 대비 두 자릿수(100배) 수준의 메모리 용량 도약을 의미한다.

```
Our results (section 4) indicate that memory layers improve the factual accuracy of language models by over
100% as measured by factual QA benchmarks, while also improving significantly on coding (HumanEval, MBPP)
and general knowledge (Hellaswag, MMLU). In many cases, memory augmented models can match the
performance of dense models that have been trained on 4x more compute. They also outperform mixture-of-experts
architectures with matching compute and parameter size, especially on factual tasks.
```
**번역**:  
우리의 결과(섹션 4)는 메모리 레이어가 사실 QA 벤치마크에서 측정했을 때 언어 모델의 사실 정확도를 100% 이상 향상시키며, 코딩(HumanEval, MBPP) 및 일반 지식(Hellaswag, MMLU)에서도 큰 개선을 보인다는 점을 보여준다. 많은 경우, 메모리로 보강된 모델은 4배 더 많은 계산량을 사용해 학습된 밀집 모델의 성능과 맞먹는다. 또한 메모리 모델은 동일한 계산량과 파라미터 크기를 갖춘 Mixture-of-Experts 아키텍처를, 특히 사실 관련 과제에서 능가한다.

```
Given these findings, we strongly advocate that memory layers should be integrated into all next generation AI
architectures.
```
**번역**:  
이러한 발견을 바탕으로, 우리는 메모리 레이어가 차세대 AI 아키텍처 전반에 통합되어야 한다고 강하게 주장한다.

---

### 2 Relatedwork

```
Language model scaling laws (Kaplan et al., 2020) study the empirical performance of language models as they
are scaled in compute, data, and parameter size. Scaling laws are typically formulated in terms of training/test
log likelihood, which is generally believed to correlate well with downstream performance. Scaling plots on
downstream tasks are also not without precedent (Brown et al., 2020), but have sometimes been shown to
exhibit non-linear behaviour and phase transitions (Wei et al., 2022; Ganguli et al., 2022). Nevertheless,
given a well behaved metric (such as task likelihood loss), most tasks exhibit smooth improvements with
scaling (Schaeffer et al., 2023).
```
**번역**:  
언어 모델 스케일링 법칙(Kaplan et al., 2020)은 언어 모델이 계산량, 데이터, 파라미터 크기 면에서 확장될 때의 실증적 성능을 연구한다. 스케일링 법칙은 일반적으로 학습/테스트 로그 확률(우도)을 기준으로 공식화되며, 이는 다운스트림 성능과 잘 상관한다고 여겨진다. 다운스트림 과제에서의 스케일링 그래프 역시 선행 연구가 없진 않다(Brown et al., 2020). 하지만 비선형적 거동이나 위상 전이(phase transition)가 나타날 때도 있다고 보고되었다(Wei et al., 2022; Ganguli et al., 2022). 그럼에도, 과제 우도 손실(task likelihood loss)과 같은 지표가 양호할 경우 대부분의 과제는 스케일 확장에 따라 점진적 향상을 보인다(Schaeffer et al., 2023).

```
Kaplan et al. (2020) showed that performance scales log-linearly with compute and parameter size across a
wide range of architecture hyper-parameters, such as model depth and width. It has been difficult to find
architectures which substantially deviate from these laws. Mixture-of-experts (MOE) (Shazeer et al., 2017;
Lepikhin et al., 2020) is a notable exception. MOE adds extra parameters to the model without increasing the
computation budget. While scaling laws for MOE also mostly focus on training perplexity, gains transfer well
to downstream applications, as evidenced by the popularity of MOE architectures in recent state-of-the-art
model families (Jiang et al., 2024; OpenAI et al., 2024; Team et al., 2024). Nevertheless, scaling laws for
specific task families and capabilities like factuality remain understudied.
```
**번역**:  
Kaplan et al. (2020)은 모델 깊이와 폭 같은 폭넓은 아키텍처 하이퍼파라미터 전반에서, 성능이 계산량과 파라미터 크기에 대해 로그선형적으로 증가함을 보였다. 이 법칙에서 크게 벗어나는 아키텍처를 찾기는 어려웠다. 그러나 Mixture-of-experts (MOE) (Shazeer et al., 2017; Lepikhin et al., 2020)는 주목할 만한 예외다. MOE는 추가 계산 예산 없이 모델에 추가 파라미터를 더한다. MOE에 대한 스케일링 법칙 역시 주로 학습 퍼플렉시티에 초점을 맞추지만, 그 성능 향상은 다운스트림 적용에도 잘 전이되며, 이는 최신 최첨단 모델 계열에서 MOE 아키텍처가 널리 사용되는 사실로 확인할 수 있다(Jiang et al., 2024; OpenAI et al., 2024; Team et al., 2024). 그럼에도, 사실성(factuality) 같은 특정 과제 계열과 능력에 대한 스케일링 법칙 연구는 여전히 미진하다.

```
Like MOE, memory augmented models also aim to augment the parameter space of the model without
adding significant computational cost. Memory networks were proposed initially in (Weston et al., 2015), and
with end-to-end training in (Sukhbaatar et al., 2015). Neural Turing Machines (Graves et al., 2014, 2016)
combine external trainable memory with other components to build a neural trainable computer. Product-key
networks (Lample et al., 2019) were introduced to make the memory lookup more efficient and scalable. The
recent PEER (He, 2024) builds on this work, replacing vector values with rank-one matrices, forming a bridge
between memory architectures and MOE.
```
**번역**:  
MOE와 마찬가지로, 메모리로 보강된 모델 역시 큰 계산 비용 없이 모델의 파라미터 공간을 확장하려고 한다. 메모리 네트워크는 (Weston et al., 2015)에서 처음 제안되었고, (Sukhbaatar et al., 2015)에서는 엔드-투-엔드 학습이 가능해졌다. Neural Turing Machines(Graves et al., 2014, 2016)는 외부 학습 가능 메모리를 다른 구성 요소와 결합하여 신경망 기반 학습 컴퓨터를 구축했다. Product-key networks(Lample et al., 2019)는 메모리 조회를 더 효율적이고 확장 가능하게 만들기 위해 도입되었다. 최근의 PEER(He, 2024)는 이 연구를 확장하여, 벡터 값을 랭크-1 행렬로 대체함으로써 메모리 아키텍처와 MOE 사이의 교량 역할을 한다.

```
Factual text generation has long been considered a fundamental capability for generative models, typically
benchmarked through factual open domain question answering (Chen et al., 2017; Chen and Yih, 2020) and
other knowledge-intensive tasks (Petroni et al., 2021). Being able to memorize the facts in the training corpus
enables the model to answer fact-seeking, knowledge intensive tasks more factually and accurately. Indeed
larger models have been shown to be more factual (Roberts et al., 2020; Brown et al., 2020), but even modern
LLMs are known to struggle with hallucination (Ji et al., 2023).
```
**번역**:  
사실성 텍스트 생성은 오래 전부터 생성 모델의 근본적 능력으로 여겨져 왔으며, 주로 사실성 개방 도메인 QA(Chen et al., 2017; Chen and Yih, 2020)와 기타 지식 집약적 과제(Petroni et al., 2021)를 통해 벤치마크되어 왔다. 훈련 말뭉치(corpus)의 사실을 암기할 수 있다는 것은 모델이 사실성·지식 집약 과제에 대해 더 정확한 답변을 할 수 있게 해준다. 실제로 더 큰 모델이 더 사실적이라는 연구 결과가 있으며(Roberts et al., 2020; Brown et al., 2020), 그럼에도 최신 LLM조차 환각(hallucination)에 어려움을 겪는 것으로 알려져 있다(Ji et al., 2023).

```
A tested way of ensuring more factuality is
through retrieval augmented generation (Lewis et al., 2021; Karpukhin et al., 2020; Lee et al., 2019; Guu et al.,
2020; Khandelwal et al., 2020). We use short-form QA tasks in this work to demonstrate the effectiveness
of memory layers and leave the long-form generation tasks for future work. Recently, a wide literature has
emerged in mitigating LLM hallucinations through data related methods, architecture variants, pre-training
and inference time improvements. We refer to (Ji et al., 2023) section 5 for a comprehensive survey.
```
**번역**:  
더 높은 사실성을 보장하는 한 가지 검증된 방법은, Retrieval-Augmented Generation(Lewis et al., 2021; Karpukhin et al., 2020; Lee et al., 2019; Guu et al., 2020; Khandelwal et al., 2020)을 이용하는 것이다. 우리는 본 연구에서 메모리 레이어의 효과를 시연하기 위해 짧은 형태의 QA 과제를 사용하고, 긴 형태의 생성 과제는 미래 연구로 남긴다. 최근에는 데이터 관련 기법, 아키텍처 변형, 사전학습 및 추론 시 개선을 통해 LLM 환각을 완화하려는 방대한 연구들이 쏟아지고 있다. 이에 대한 종합적인 개요는 (Ji et al., 2023)의 섹션 5를 참조하라.

---

### 3 MemoryAugmentedArchitectures

```
Trainable memory layers work similarly to the ubiquitous attention mechanism (Bahdanau et al., 2016). Given
a query q ∈ Rn, a set of keys K ∈ RN×n and values V ∈ RN×n, the output is a soft combination of values,
weighted according to the similarity between q and the corresponding keys. Two major differences separate
memory layers from attention layers as they are typically used (Vaswani et al., 2023). First, the keys and
values in memory layers are trainable parameters, as opposed to activations. Second, memory layers typically
have larger scale in terms of the number of keys and values, making sparse lookup and updates a necessity.
```
**번역**:  
학습 가능한 메모리 레이어는, 널리 쓰이는 어텐션 메커니즘(Bahdanau et al., 2016)과 유사하게 작동한다. 쿼리 q ∈ R^n, 키 집합 K ∈ R^(N×n), 값 집합 V ∈ R^(N×n)이 주어졌을 때, 출력은 q와 해당 키 간의 유사도에 따라 가중이 부여된 값들의 소프트 조합이다. 전형적인 사용 방식의 어텐션 레이어와 메모리 레이어를 구분하는 주요 차이점은 두 가지다(Vaswani et al., 2023). 첫째, 메모리 레이어의 키와 값은 활성화(activation)가 아닌 **학습 가능한 파라미터**라는 점이다. 둘째, 메모리 레이어는 보통 훨씬 더 많은 키와 값을 갖기 때문에, 희소 조회(sparse lookup)와 갱신이 필수적이다.

```
For example in this work, we scale the number of key-value pairs to several millions. In this case, only the
top-k most similar keys and corresponding values take part in the output. A simple memory layer can be
described by the following equations:
```
**번역**:  
예를 들어 본 연구에서는, 키-값 쌍의 개수를 수백만 수준으로 확장한다. 이런 경우, 가장 유사도가 높은 상위 k개의 키와 해당 값들만 출력에 관여하게 된다. 간단한 메모리 레이어는 다음과 같은 방정식으로 표현할 수 있다:

```
I =SelectTopkIndices(Kq),
s =Softmax(KIq),
y =sVI
(1)
```
**번역**(수식 설명):  
- I = SelectTopkIndices(Kq) : 키 행렬 K와 쿼리 q의 곱(Kq)을 이용해 상위 k개 인덱스를 선택  
- s = Softmax(K_I q) : 선택된 키 K_I와 쿼리 q의 내적을 소프트맥스로 변환  
- y = s V_I : 해당 값 벡터 V_I에 s를 가중으로 주어 합산한 결과가 최종 출력 y

```
Here I is a set of indices, s ∈ Rk, KI,VI ∈ Rk× n, and the output y ∈ Rn. Each token embedding (for us, the
output of the previous attention layer) goes through this memory lookup independently, similar to the FFN
operation that we replace.
```
**번역**:  
여기서 I는 인덱스 집합이고, s ∈ R^k, K_I, V_I ∈ R^(k×n)이며, 최종 출력 y는 R^n에 속한다. 각 토큰 임베딩(본 연구에서는 이전 어텐션 레이어의 출력)은, 우리가 대체하는 FFN 연산과 유사하게, 이 메모리 조회 과정을 독립적으로 거치게 된다.

---

#### 3.1 Scalingmemorylayers

```
Being light on compute, and heavy on memory, memory layers have distinct scaling challenges. We detail
some of these challenges and how we address them in this section.
```
**번역**:  
계산량은 적지만 메모리 사용이 많은 메모리 레이어는 고유한 확장상의 과제를 안고 있다. 본 절에서는 이러한 과제 중 일부와, 이를 해결하는 우리의 접근 방식을 자세히 설명한다.

##### 3.1.1 Product-keylookup

```
One bottleneck which arises when scaling memory layers is the query-key retrieval mechanism. A naive
nearest-neighbour search requires comparing each query-key pair, which quickly becomes prohibitive for large
memories. While fast approximate vector similarity techniques (Johnson et al., 2019) could be used here, it’s a
challenge to incorporate them when the keys are being continually trained and need to be re-indexed. Instead,
we adopt trainable product-quantized keys from (Lample et al., 2019).
```
**번역**:  
메모리 레이어를 확장할 때 발생하는 한 가지 병목은 쿼리-키 검색 메커니즘이다. 단순 근접 이웃 검색을 사용하면 모든 쿼리-키 쌍을 비교해야 하므로, 대규모 메모리를 다룰 때 매우 비효율적이다. 빠른 근사 벡터 유사도 기법(Johnson et al., 2019)을 사용할 수도 있지만, 키가 지속적으로 학습되고 재인덱싱되어야 하는 상황에 이를 통합하기는 어렵다. 대신 우리는 (Lample et al., 2019)에서 제안된 **학습 가능한 프로덕트-양자화 키**(product-quantized keys)를 채택한다.

```
Product keys work by having two sets
of keys instead of one, where K1,K2 ∈ R^(√N×n). The full set of keys of size N×n, which is never instantiated,
consists of the product of these two sets. The top-k lookup on the full set of keys can be efficiently done by
searching the much smaller set of half-keys first, saving compute and memory.
```
**번역**:  
프로덕트 키는 하나의 키 세트 대신 두 개의 키 세트를 사용하여 동작하는데, 여기서 K1, K2는 R^(√N×n)에 속한다. 크기가 N×n인 전체 키 집합은 실제로 완전히 생성되지 않으며, 이 두 세트의 곱으로 구성된다. 전체 키 집합에서의 top-k 조회는 훨씬 작은 크기의 절반 키(half-keys)를 먼저 검색함으로써 효율적으로 수행되어, 계산과 메모리를 절약한다.

```
To perform the lookup, we
first split the query as q1,q2 ∈ R^(n/2). Let I1,I2 and s1,s2 be the top-k indices and scores obtained from the
respective key sets K1,K2. Since there are only √N keys in each set, this operation is efficient. The overall
indices and scores can be found by taking argmax(i1∈I1,i2∈I2)(s1[i1] + s2[i2]).
```
**번역**:  
조회 수행을 위해 쿼리를 먼저 q1, q2 ∈ R^(n/2)로 분할한다. I1, I2와 s1, s2를 각각 키 세트 K1, K2에서 구한 top-k 인덱스와 점수라고 하자. 각 세트에 있는 키가 √N개뿐이므로, 이 연산은 효율적이다. 전체 인덱스와 점수는 (s1[i1] + s2[i2])를 최대로 만드는 (i1 ∈ I1, i2 ∈ I2)에 대한 argmax를 취해 구할 수 있다.

##### 3.1.2 Parallel memory

```
Memory layers are naturally memory-intensive, mostly due to the large number of trainable parameters
and associated optimizer states. To implement them at the scale of several millions of keys, we parallelize
the embedding lookup and aggregation across multiple GPUs. The memory values are sharded across the
embedding dimension. At each step, the indices are gathered from the process group, each worker does a
lookup and then aggregates the portion of embeddings in its own shard.
```
**번역**:  
메모리 레이어는 기본적으로 매우 많은 학습 가능한 파라미터와 이와 연관된 옵티마이저 상태 때문에 메모리 사용량이 크다. 수백만 개의 키 규모로 구현하려면, 임베딩 조회와 집계를 여러 GPU에 걸쳐 병렬화해야 한다. 메모리 값들은 임베딩 차원을 기준으로 나누어(shard) 저장된다. 각 단계마다 인덱스가 프로세스 그룹에서 모이고, 각 워커는 해당 인덱스에 대해 조회를 수행한 뒤, 자기 샤드에 해당하는 임베딩 부분을 집계한다.

```
After this, each worker gathers
the partial embeddings corresponding to its own portion of the indices. We take care to keep activation
memory manageable at this stage, by making sure each GPU only gets its own portion, and does not need
to instantiate the entire embedding output. The process is illustrated in figure 2.
```
**번역**:  
그 다음 각 워커는, 자기 인덱스 부분에 해당하는 임베딩 조각을 수집한다. 우리는 이 단계에서 각 GPU가 자기 부분만 받도록 하여, 전체 임베딩 출력을 한 번에 메모리에 올리지 않도록 주의해, 활성화(activation) 메모리를 관리 가능한 수준으로 유지한다. 이 과정을 그림 2에 나타냈다.

```
The implementation is
independent of other model parallelism schemes such as tensor, context or pipeline parallelism, and operates
on its own process group.
```
**번역**:  
이 구현은 텐서 병렬화, 컨텍스트 병렬화, 파이프라인 병렬화 같은 다른 모델 병렬화 방식과 무관하게 자체 프로세스 그룹에서 동작한다.

```
GPU-0
 idx A
 idx B
 idx C
 GPU-1
 idx D
 idx E
 A
 B
 D
 E
 C
 A
 B
 D
 E
 C
 Share 
indexes
 D
 E
 C
 Share 
indexes
 idx A
 idx B
 idx C
 idx D
 idx E
 idx A
 idx B
 idx C
 idx D
 idx E
 A
 B
 D
 E
 C
 A
 B
 D
 E
 C
 Send 
Embeddings
 Send 
Embeddings
 A
 B
 C
 D
 E
 Figure 2 Illustration of the parallel EmbeddingBag implementation for a “Memory Group” of two GPUs. Each GPU
 performs the EmbeddingBag operation on all of the indices of the group, but on half-dimension embeddings it has
 access to.
```
**번역(그림 설명)**:  
그림 2: 2개의 GPU로 구성된 “Memory Group”에서 병렬 EmbeddingBag 구현 예시. 각 GPU는 그룹의 모든 인덱스에 대한 EmbeddingBag 연산을 수행하지만, 자기 GPU에 할당된 절반 차원의 임베딩만 접근·연산한다.

##### 3.1.3 Sharedmemory

```
Deep networks encode information at different levels of abstraction across different layers. Adding memory
to multiple layers may help the model use its memory in more versatile ways. In contrast to previous
work (Lample et al., 2019), we use a shared pool of memory parameters across all memory layers, thus keeping
parameter count the same and maximizing parameter sharing.
```
**번역**:  
심층 신경망은 서로 다른 레이어에서 서로 다른 수준의 추상화로 정보를 인코딩한다. 여러 레이어에 메모리를 추가하면, 모델이 더 다재다능한 방식으로 메모리를 활용할 수 있을 것이다. (Lample et al., 2019)와 달리, 우리는 모든 메모리 레이어에 걸쳐 **공유 메모리 파라미터 풀**을 사용하여, 파라미터 수를 동일하게 유지하면서 공유를 극대화한다.

```
We find that multiple memory layers increase
performance significantly over having a single layer with the same total parameter count, up to a certain
number of layers (in our case, 3). Beyond this point, replacing further FFN layers degrades performance,
showing sparse and dense layers are both needed and likely complementary (see section 5.4).
```
**번역**:  
이렇게 하면, 동일한 전체 파라미터 수에서 단일 메모리 레이어를 사용하는 것보다 여러 메모리 레이어를 사용하는 편이 성능을 유의미하게 개선시킨다. 다만 일정 개수(우리 사례에서는 3개)를 초과하면, 추가로 FFN 레이어를 대체할수록 성능이 떨어진다. 이는 희소 레이어와 밀집 레이어가 모두 필요하며 상호보완적이라는 점을 시사한다(섹션 5.4 참고).

##### 3.1.4 Performanceandstabilityimprovements

```
The main operations in the memory layer is to compute the weighted sum of the top-k embeddings: it is
implemented in PyTorch’s EmbeddingBag operation. As the number of floating-point operations is negligible,
we expect this operation to be solely limited by the GPU memory bandwidth, but find multiple inefficiencies
in PyTorch’s implementation in practice.
```
**번역**:  
메모리 레이어의 주요 연산은 top-k 임베딩의 가중 합을 계산하는 것으로, 이는 PyTorch의 EmbeddingBag 연산에서 구현된다. 부동소수점 연산 횟수가 매우 적기 때문에, 이 연산은 GPU 메모리 대역폭에 의해서만 제한될 것으로 예상된다. 하지만 실제로는 PyTorch 구현에 여러 비효율이 존재함을 발견했다.

```
We implemented new and more efficient CUDA kernels for this
operation. Our forward pass optimizes memory accesses and achieves 3TB/s of memory bandwidth, which is
close to our H100 specification of 3.35TB/s (compared to less than 400GB/s with PyTorch’s implementation).
```
**번역**:  
우리는 이 연산을 위해 새로운, 더 효율적인 CUDA 커널을 구현했다. 우리의 포워드 패스는 메모리 접근을 최적화하여 초당 3TB의 메모리 대역폭을 달성했는데, 이는 H100 사양인 초당 3.35TB에 근접한 수치다(기존 PyTorch 구현의 경우 초당 400GB 미만과 비교).

```
The backward pass is more complicated as multiple output gradients have to be propagated to the same
weight gradient. We benchmarked multiple strategies: accumulation via atomic additions ("atomics"), row
level atomic lock where we amortize the cost of memory lock over the embedding dimension ("lock"), and
atomic-free("reverse_indices").
```
**번역**:  
역전파 단계는 여러 출력 그라디언트가 동일한 가중치 그라디언트로 전달되어야 하므로 더 복잡하다. 우리는 여러 전략을 벤치마킹했는데, 원자적 덧셈(“atomics”)을 통한 누적, 임베딩 차원에 걸쳐 메모리 잠금 비용을 분산시키는 행 단위 원자 잠금(“lock”), 그리고 원자 연산 없이 진행하는(“reverse_indices”) 기법 등이 그것이다.

```
The latter approach requires some preprocessing to inverse the token_idto
embedding_id mapping, so that each row in the embedding gradient can know which token will contribute to
it. Typically, while the "atomics" approach is already up to 5x faster than the existing PyTorch operator, we
found that the "reverse_indices" and "lock" approaches can be faster when the embedding dimension exceeds
128, as long as the embeddings are roughly balanced.
```
**번역**:  
마지막 접근법은 token_id를 embedding_id 매핑의 역으로 바꾸는 전처리가 필요하며, 이를 통해 임베딩 그라디언트의 각 행이 어떤 토큰이 기여하는지 알 수 있게 된다. 일반적으로 “atomics” 방식도 기존 PyTorch 연산자보다 최대 5배까지 빠르지만, “reverse_indices”나 “lock” 방식이 임베딩 차원이 128을 넘고, 임베딩이 대체로 균형 잡혀 있다면 더 빠를 수 있음을 발견했다.

```
Overall, our custom kernels make the embeddingbag
operation end-to-end 6x faster compared to PyTorch’s EmbeddingBag for our usecases.
```
**번역**:  
결과적으로, 우리의 커스텀 커널은 우리의 사용 사례에서, EmbeddingBag 연산을 PyTorch 기본 구현 대비 종단 간(end-to-end)으로 6배 빠르게 만들어 준다.

```
We improve training performance of the memory layer by introducing input-dependent gating with a silu
non-linearity (Hendrycks and Gimpel, 2023). The output in equation (1) then becomes
```
**번역**:  
우리는 입력 의존 게이팅(gating)과 silu 비선형성(Hendrycks and Gimpel, 2023)을 도입하여 메모리 레이어의 학습 성능을 개선했다. 이로 인해 식 (1)의 출력은 다음과 같이 변한다.

```
output=(y⊙silu(xTW1))TW2 (2)
where silu(x)=x·sigmoid(x) and ⊙ is the element-wise multiplication (see also figure3).
```
**번역(수식)**:  
\[
\text{output} = (\,y \,\odot\, \text{silu}(x^T W_1)\,)^T W_2
\]  
단, \(\text{silu}(x) = x \cdot \sigma(x)\) 이고, \(\odot\)는 요소별 곱이다. (그림 3도 참조)

```
We find that for large
memory layers, training can become unstable, especially for small base models. We use qk-normalization (Team,
2024) when needed to alleviate this issue.
```
**번역**:  
우리는 큰 메모리 레이어를 사용할 때, 특히 작은 베이스 모델에서 학습이 불안정해질 수 있음을 발견했다. 이런 문제를 완화하기 위해 필요할 때 qk-normalization(Team, 2024)을 사용한다.

```
Self-Attention
Query MLP
Sub Key1
Sub Key2
top-k
Values
Self-Attention
Query MLP
Sub Key1
Sub Key2
top-k
Values
W1
W2
silu
RMSNorm RMSNorm
RMSNorm RMSNorm
softmax softmax
Figure3Onthelefttheregularmemorylayer.Ontheright, theMemory+block,withtheaddedprojection,gating
andsilunon-linearity
```
**번역(그림 설명)**:  
그림 3: 왼쪽은 일반 메모리 레이어이고, 오른쪽은 프로젝션·게이팅·silu 비선형성이 추가된 Memory+ 블록을 나타낸다.

---

### 4 Experimentalsetup

```
For our base model architecture, we follow closely the Llama series of dense transformers (Touvron et al., 2023;
Dubey et al., 2024), which also serve as our dense baselines. We augment the base models by replacing one or
more of the feed-forward layers with a shared memory layer. For scaling law experiments, we pick base model
sizes of 134m, 373m, 720m, and 1.3b parameters. For these models, we use the Llama2 tokenizer with 32k
tokens, and train to 1T tokens with a pretraining data mix that is similar to that of Llama2 (Touvron et al.,
2023). For experiments at the 8B base model scale, we use the Llama3 (Dubey et al., 2024) configuration and
tokenizer (128k tokens), and a better optimized data mix similar to Llama3.
```
**번역**:  
우리의 베이스 모델 아키텍처는 Llama 계열의 밀집 트랜스포머(Touvron et al., 2023; Dubey et al., 2024)를 가깝게 따르며, 이는 동시에 우리의 밀집 모델 기준선 역할을 한다. 우리는 베이스 모델에서 하나 이상의 피드포워드 레이어를 공유 메모리 레이어로 교체하여 보강한다. 스케일링 법칙 실험을 위해, 1억3천4백만(134m), 3억7천3백만(373m), 7억2천만(720m), 13억(1.3b) 파라미터 모델을 선택한다. 이러한 모델들은 Llama2 토크나이저(32k 토큰)를 사용하고, Llama2(Touvron et al., 2023)와 유사한 사전학습 데이터 혼합으로 1조(1T) 토큰까지 학습된다. 80억(8B) 베이스 모델 규모의 실험에서는 Llama3(Dubey et al., 2024) 구성 및 토크나이저(128k 토큰)를 사용하고, Llama3와 유사한 더 최적화된 데이터 혼합을 사용한다.

#### 4.1 Baselines

```
In addition to the dense baselines, we also compare to other parameter augmentations including mixture-of
experts (MOE) (Shazeer et al., 2017) and the more recent PEER (He, 2024) model. In MOE, each FFN layer
is composed of multiple “experts”, only a subset of which participate in the computation for each input. The
PEER model is conceptually similar to a memory layer, but instead of retrieving a single value embedding, it
retrieves a pair of embeddings, which combine into a rank-1 matrix.
```
**번역**:  
우리는 밀집 모델 기준선 외에도, Mixture-of-Experts(MOE)(Shazeer et al., 2017)와 최근의 PEER(He, 2024) 모델 등 다른 파라미터 증강 기법과 비교한다. MOE에서는 각 FFN 레이어가 여러 “전문가(expert)”로 구성되며, 각 입력마다 일부 전문가만 계산에 참여한다. PEER 모델은 개념적으로 메모리 레이어와 유사하지만, 단일 값 임베딩을 조회하는 대신 임베딩 한 쌍을 조회하여 랭크-1 행렬을 형성한다.

```
Several of these are assembled together
into a dynamic feed-forward layer. PEER works similarly to memory layers in practice, but requires twice
the number of parameters for the same number of keys. Like memory layers, these methods increase the
number of parameters in the model without significantly increasing FLOPs.
```
**번역**:  
이 임베딩 쌍 여러 개가 모여 동적으로 피드포워드 레이어를 구성한다. PEER는 실제로 메모리 레이어와 비슷하게 동작하지만, 동일한 키 개수에 대해 두 배의 파라미터가 필요하다. 메모리 레이어와 마찬가지로, 이런 방식들도 FLOPs를 크게 늘리지 않고 모델의 파라미터 수를 늘린다.

```
We pick the number of experts
in MOE and the number of keys in PEER to match the number of parameters of our memory-augmented
models as closely as possible. MOE models are trained with expert choice (Zhou et al., 2022), and evaluated
with top-1 routing. PEER layers share the same configuration and hyper-parameters as our memory layer
implementation.
```
**번역**:  
우리는 MOE의 전문가(expert) 수와 PEER의 키 수를, 우리의 메모리 보강 모델의 파라미터 수에 최대한 가깝게 맞춘다. MOE 모델은 expert choice(Zhou et al., 2022)를 사용해 학습되고, 추론 시 top-1 라우팅을 사용한다. PEER 레이어는 우리의 메모리 레이어 구현과 동일한 구성과 하이퍼파라미터를 공유한다.

#### 4.2 Evaluationbenchmarks

```
Our evaluations cover factual question answering (NaturalQuestions (Kwiatkowski et al., 2019), TriviaQA (Joshi
et al., 2017)), multi-hop question answering (HotpotQA (Yang et al., 2018)), scientific and common sense
world knowledge (MMLU (Hendrycks et al., 2021), HellaSwag (Zellers et al., 2019), OBQA (Mihaylov et al.,
2018), PIQA (Bisk et al., 2019)) and coding (HumanEval (Chen et al., 2021), MBPP (Austin et al., 2021)).
```
**번역**:  
우리는 평가로 사실성 QA(NaturalQuestions(Kwiatkowski et al., 2019), TriviaQA(Joshi et al., 2017)), 멀티홉 QA(HotpotQA(Yang et al., 2018)), 과학적·상식적 세계 지식(MMLU(Hendrycks et al., 2021), HellaSwag(Zellers et al., 2019), OBQA(Mihaylov et al., 2018), PIQA(Bisk et al., 2019)) 그리고 코딩(HumanEval(Chen et al., 2021), MBPP(Austin et al., 2021)) 등을 아우른다.

```
We try to report the most commonly used accuracy metrics (exact match or F1 score for QA benchmarks,
pass-at-1 for coding). For some bencmarks, the performance of small models can be very low, and accuracy
numbers noisy. Therefore we use negative log-likelihood (nll) of the correct answer for model ablations.
```
**번역**:  
우리는 가능한 한 널리 쓰이는 정확도 지표(QA 벤치마크에는 exact match 또는 F1, 코딩에는 pass@1)를 보고하려고 한다. 일부 벤치마크에서는 작은 모델 성능이 매우 낮아 정확도 수치가 노이즈가 클 수 있다. 따라서 모델 구조를 비교(ablations)할 때는 정답의 음의 로그가능도(nll)를 활용한다.

---

### 5 Scalingresults

```
We compare Memory models to baselines in a compute-controlled setting.
```
**번역**:  
우리는 계산량이 통제된 조건에서 메모리 모델을 기준선과 비교한다.

#### 5.1 Withfixedmemorysize

```
First, we fix the size of the memory, and therefore the number of extra parameters, and compare with the
dense baseline, as well as roughly parameter matched MOE and PEER models. Models with the same base
model configuration have negligible differences in FLOPs. For Memory models, we fix the number of half
keys to 2^10, and thus the number of memory values to 2^20 (roughly 1 million). For the PEER baseline, we
pick the number of half-keys to be 768, resulting in slightly more total parameters than Memory. For MOE
models, we pick the lowest number of experts such that the parameter count exceeds that of Memory. This
corresponds to 16, 8, 6, and 4 experts for the 134m, 373m, 720m and 1.3b sizes respectively.
```
**번역**:  
먼저, 메모리 크기(즉 추가 파라미터 수)를 고정하고, 이를 밀집 기준선 및 대략적으로 파라미터를 맞춘 MOE, PEER 모델과 비교한다. 동일한 베이스 모델 구성을 가진 모델들은 FLOPs 차이가 무시할 만하다. 메모리 모델의 경우, 우리는 하프 키(half-keys) 수를 2^10으로 고정했고, 따라서 메모리 값(memory values) 수는 2^20(약 백만)으로 설정했다. PEER 기준선에서는 하프 키 수를 768로 두어, Memory 모델보다 약간 더 많은 전체 파라미터가 되도록 했다. MOE 모델의 경우, 파라미터 수가 Memory 모델보다 많아지도록 하면서 가장 낮은 전문가(expert) 수를 선택했는데, 이는 각기 134m, 373m, 720m, 1.3b 모델 크기에 대해 16, 8, 6, 4명의 전문가에 해당한다.

```
The vanilla Memory model has a single memory layer, which we pick to replace the middle FFN layer of the
transformer. Our improved Memory+ model has 3 memory layers, placed centered with a stride of 4 for the
134m models and 8 for the others. Additionally it includes a custom swilu non-linearity, and optimized key
dimension (set to equal half of the value dim). As noted earlier, memory layers share parameters, thus have
identical memory footprint to a single memory layer.
```
**번역**:  
기본(Vanilla) Memory 모델은 단일 메모리 레이어를 사용하며, 트랜스포머의 중간 FFN 레이어를 대체한다. 우리가 개선한 Memory+ 모델은 3개의 메모리 레이어를 가지며, 134m 모델에는 stride 4로, 나머지 모델에는 stride 8로 중앙에 배치한다. 여기에 맞춤형 swilu 비선형성과 최적화된 키 차원(값 차원의 절반)도 포함된다. 앞서 언급했듯, 메모리 레이어들은 파라미터를 공유하므로, 단일 메모리 레이어와 동일한 메모리 사용량을 가진다.

```
Wecan see from table 1 that Memory models improve drastically over the dense baselines, and generally match
the performance of models with twice the number of dense parameters on QA tasks. Memory+ improves
further over Memory, with performance falling generally between dense models with 2x-4x higher compute.
The PEER architecture performs similarly to Memory for the same number of parameters, while lagging
behind Memory+. MOE models underperform the memory variants by large margins. figure 4 shows the
scaling performance of Memory, MOE and dense models on QA tasks across various base model sizes.
```
**번역**:  
표 1에서 확인할 수 있듯이, 메모리 모델은 밀집 기준선을 크게 능가하며, 일반적으로 두 배 많은 밀집 파라미터를 가진 모델의 QA 과제 성능과 맞먹는다. Memory+는 Memory보다 더욱 개선되어, 대략 2배~4배 더 많은 계산량을 사용한 밀집 모델 사이의 성능 범위에 위치한다. PEER 아키텍처는 같은 파라미터 수에서 Memory와 유사한 성능을 내지만, Memory+에는 뒤처진다. MOE 모델은 메모리 계열에 크게 못 미친다. 그림 4는 다양한 베이스 모델 크기에 걸쳐 QA 과제에서 Memory, MOE, 밀집 모델의 스케일링 성능을 보여준다.

```
NaturalQuestions
15
Accuracy (%)
10
5
0
Memory+
MOE
Dense
134m
373m 720m 1.3b
Base Parameters
TriviaQA
40
f1-score
20
Memory+
MOE
Dense
0
124m
373m 720m 1.3b
Base Parameters
Figure 4 Accuracy vs. Base Parameters for NaturalQuestions and TriviaQA (Memory+ models use 1 million memory
embeddings.)
```
**번역(그림 설명)**:  
그림 4: NaturalQuestions와 TriviaQA에 대한 정확도 대비 베이스 파라미터 크기. (Memory+ 모델은 100만 개의 메모리 임베딩을 사용)

---

#### 5.2 Scalingmemorysizewithafixedbasemodel

```
Next, we investigate scaling behaviour with respect to the memory size for a fixed base model. In figure 1, we
see that factual QA performance for a Memory+ model keeps increasing predictably with increasing memory
size. At 64 million keys (128 billion memory parameters), a 1.3b Memory model approaches the performance
of the Llama2 7B model, that has been trained on 2x more tokens using 10x more FLOPs. (see also table 2).
```
**번역**:  
다음으로, 베이스 모델을 고정했을 때 메모리 크기를 확장하는 경우의 스케일링 거동을 살펴본다. 그림 1에서, Memory+ 모델의 사실 QA 성능은 메모리 크기가 증가함에 따라 예측 가능하게 계속 상승하는 것을 볼 수 있다. 6400만 개 키(메모리 파라미터 1,280억)에서, 13억(1.3b) Memory 모델은 2배 더 많은 토큰과 10배 더 많은 FLOPs로 학습된 Llama2 70억(7B) 모델의 성능에 근접한다(표 2도 참고).

#### 5.3 Resultsat8Bscale

```
Finally, we scale our Memory+ model with an 8B base model and 40962 memory values (64B memory
parameters). We use the Llama3 8B (Dubey et al., 2024) architecture and tokenizer, and train on a data
mix similar to Llama3 (Dubey et al., 2024). We report results at 200 billion and 1 trillion tokens of training
in table 2.
```
**번역**:  
마지막으로, 우리는 80억(8B) 베이스 모델과 4096^2(약 1677만) → (원문 40962는 4096^2 표기 추정)개의 메모리 값을 사용하여(대략 640억(64B) 메모리 파라미터) Memory+ 모델을 확장한다. Llama3 8B(Dubey et al., 2024) 아키텍처와 토크나이저를 사용하고, Llama3와 유사한 데이터 혼합으로 학습한다. 2000억(200B) 토큰과 1조(1T) 토큰 학습 시점의 결과를 표 2에 제시한다.

```
On an expanded set of benchmarks, including general scientific and world knowledge and coding, we
see that memory augmented models significantly outperform dense baselines. The gains are more pronounced
earlier in training (200B tokens), suggesting that memory helps models learn facts faster. At only 1 trillion
tokens of training, our Memory+ model approaches the performance of Llama3.1 8B, which was trained on
15 trillion tokens.
```
**번역**:  
과학 및 일반 세계 지식, 코딩 등을 포함하는 더 확장된 벤치마크에서, 메모리로 보강된 모델은 밀집 기준선을 크게 능가한다. 이러한 성능 향상은 학습 초반(2000억 토큰)에서 특히 두드러지며, 이는 메모리가 모델이 사실을 더 빠르게 학습하도록 돕는다는 점을 시사한다. 1조(1T) 토큰 학습만으로, 우리의 Memory+ 모델은 15조(15T) 토큰으로 학습된 Llama3.1 8B 성능에 근접한다.

#### 5.4 Modelablations

```
In this section, we present results which motivate our modelling choices for the Memory+ architecture.
```
**번역**:  
이 절에서는 Memory+ 아키텍처에 대한 우리의 모델링 선택을 정당화하는 결과를 제시한다.

```
Memory layer placement Since the memory pool is shared, we can replace more FFN layers with memory
layers without increasing either the memory or the compute budget. We see that as we add more memory
layers, performance initially increases. However, as we’re effectively removing dense parameters from the
model for each added memory layer, eventually the model performance degrades, revealing a sweet spot at
around 3 memory layers (table 3, left).
```
**번역**:  
**메모리 레이어 배치**: 메모리 풀이 공유되므로, 메모리나 계산 예산을 늘리지 않고도 더 많은 FFN 레이어를 메모리 레이어로 교체할 수 있다. 우리는 메모리 레이어를 많이 추가할수록 성능이 초기에는 향상됨을 확인했다. 그러나 레이어 하나를 추가할 때마다 실제로 밀집 파라미터가 제거되기 때문에, 결국 모델 성능이 떨어지기 시작하며, 대략 메모리 레이어 3개일 때가 적절한 지점임을 발견했다(표 3, 왼쪽).

```
Moreover, we experiment with the placement of these layers, modifying
the centring and spacing. We find that centred placements with larger strides are better, and we adopt this
for our Memory+ architecture.
```
**번역**:  
추가로, 이 레이어들의 배치를 실험하며, 중앙 배치와 간격을 달리해 보았다. 우리는 큰 stride를 두고 레이어들을 중앙에 배치하는 것이 더 좋음을 발견했으며, 이를 우리의 Memory+ 아키텍처에 적용한다.

```
Memory layervariants Weexperimentwithminormodificationstothememorymechanism(table3, right).
Wetry1. gatingthememorywiththeinputusingalinearprojection,2. addingacustomswilunon-linearity
(figure3),3. addingrandomkey-valuepairsinadditiontothetop-kduringpre-trainingtounbiaskeyselection,
4. addingasinglefixedkey-valuepair(softmaxsink)tothetop-kselectedvaluesduringpre-trainingto
serveas"anchor".
```
**원문의 띄어쓰기 깨진 부분을 최대한 직역**:  
```
Memory layer variants. We experiment with minor modifications to the memory mechanism (table 3, right).
We try (1) gating the memory with the input using a linear projection, (2) adding a custom swilu non-linearity
(figure 3), (3) adding random key-value pairs in addition to the top-k during pre-training to unbias key selection,
(4) adding a single fixed key-value pair (softmax sink) to the top-k selected values during pre-training to
serve as an "anchor".
```
**번역**:  
**메모리 레이어 변형**: 우리는 메모리 메커니즘에 대한 몇 가지 사소한 수정 실험을 진행했다(표 3 오른쪽).  
1. 입력에 대해 선형 프로젝션을 사용하여 메모리를 게이팅(gating)하는 것  
2. 사용자 정의 swilu 비선형성(그림 3) 추가  
3. 사전 학습 시 상위 k개 이외에 임의의 키-값 쌍도 추가하여 키 선택의 편향을 줄이는 것  
4. 사전 학습 시 상위 k개로 선택된 값에 단일 고정 키-값 쌍(softmax sink)을 추가하여 “앵커” 역할을 하도록 하는 것

```
Wefindthattheswilunon-linearityconsistentlyimprovesresults, andweadoptthis
improvementintoourmodel. Simplegatingimprovesperformanceonlyinsomecases,andswilualreadycovers
thisbehaviourtosomeextent, sowedecidenottodoadditionalgating. Forkeysamplingimprovements,
includingtherandomkeysandthefixed(sink)key,weseeminorimprovements,howeverthesehavesome
negativeimpactontrainingspeedinour implementation,andthegainswerenotconsistentfor largermodel
sizes, thereforeweexcludedthemfromourexperiments, leavingthisdirectionopenforfutureexploration.
```
**원문 띄어쓰기 보정 후 번역**:  
```
We find that the swilu non-linearity consistently improves results, and we adopt this improvement into our model. 
Simple gating improves performance only in some cases, and swilu already covers this behaviour to some extent, 
so we decide not to do additional gating. For key sampling improvements, including the random keys and the fixed (sink) key, 
we see minor improvements, however these have some negative impact on training speed in our implementation, 
and the gains were not consistent for larger model sizes, therefore we excluded them from our experiments, 
leaving this direction open for future exploration.
```
**번역**:  
우리는 swilu 비선형성을 적용할 때 결과가 일관되게 개선됨을 발견했고, 이를 모델에 도입했다. 단순 게이팅은 일부 경우에만 성능이 좋아졌고, swilu 자체가 이를 어느 정도 대체하므로 별도의 게이팅은 추가하지 않기로 했다. 랜덤 키나 고정(싱크) 키를 포함한 키 샘플링 개선은 약간의 성능 향상이 있었지만, 구현 상 학습 속도가 느려지는 문제가 있고, 더 큰 모델 크기에서는 이득이 일관적이지 않았으므로, 우리는 이 부분을 실험에서 제외했고 미래 연구 과제로 남겼다.

```
nll NQnll TQAnll
layer#
12 2.11 12.13 8.34
12,16,20 2.08 11.60 7.54
8,12,16 2.07 11.79 7.64
4,12,20 2.06 11.32 7.20
5,8,11,14,17,21 2.11 11.79 7.73
```
**번역(표 왼쪽)**:  
- 레이어 배치 실험(layer#):  
  - 12번 레이어에만 메모리? NQ nll=2.11, TQA nll=12.13, 8.34  
  - 12, 16, 20번 레이어에 메모리? NQ nll=2.08, …  
  - 8, 12, 16번 레이어에 메모리? NQ nll=2.07, …  
  - 4, 12, 20번 레이어에 메모리? NQ nll=2.06, …  
  - 5, 8, 11, 14, 17, 21번 레이어(6개)에 메모리? NQ nll=2.11, …  

```
nll NQnll TQAnll
Model
PKbase 2.11 12.13 8.34
+gated 2.11 12.24 8.17
+swilu 2.11 12.05 8.09
+randomvalues 2.11 12.36 8.09
+softmaxsink 2.11 12.19 8.04
```
**번역(표 오른쪽)**:  
- 모델 변형에 따른 nll (train NLL, NQ NLL, TQA NLL):
  - PKbase (기본) vs +gated vs +swilu vs +randomvalues vs +softmaxsink

```
Table3Ablationstudies: ontheleft,numberofmemorylayerswithsharedmemory,ontherightdifferentmemory
architecturevariations.Metricsareallloglikelihood,onthetrainingset,NQanswersandTQAanswers.
```
**번역**:  
표 3: 좌측은 공유 메모리를 사용하는 메모리 레이어 개수를, 우측은 다른 메모리 아키텍처 변형을 다룬 소규모 연구다. 모든 지표는 학습 세트, NQ 답변, TQA 답변 각각의 로그우도(log likelihood)다.

---

```
KeyandvaluedimensionBydefault, thememoryvaluedimensionischosentobethesameasthebase
modeldimension.However,wecanpotentiallytrade-offthevaluedimensionwiththenumberofvaluesinthe
memorywithoutchangingthetotalparametersizeofthememoryusinganextraprojectionafterMemory.
```
**원문 띄어쓰기 보정 후 번역**:  
```
Key and value dimension. By default, the memory value dimension is chosen to be the same as the base
model dimension. However, we can potentially trade off the value dimension with the number of values in the
memory without changing the total parameter size of the memory, using an extra projection after Memory.
```
**번역**:  
**키와 값의 차원**: 기본적으로, 메모리 값(value) 차원은 베이스 모델 차원과 동일하게 설정한다. 하지만, 메모리 전체 파라미터 크기를 바꾸지 않으면서, 메모리 연산 뒤 추가 프로젝션을 사용해 값 차원과 값의 개수를 상호 교환(trade-off)할 수 있다.

```
Wepresentthisablationintable4, left,andfindthatthedefaultconfigurationisoptimal.Wecanalso
independentlyincreasethekeyembeddingdimension,whichwedointable4,right.Wefindunsurprisingly
thatincreasingthekeydimisbeneficial.However,increasingthekeydimdoesaddmoredenseparametersto
themodel,andthuswecannotincreaseitindefinitelywithoutbreakingourfaircomparisons.Wepickakey
dimensionofhalfthebasemodeldimforourexperiments.
```
**번역(띄어쓰기 보정)**:
```
We present this ablation in table 4, left, and find that the default configuration is optimal. We can also
independently increase the key embedding dimension, which we do in table 4, right. We find unsurprisingly
that increasing the key dim is beneficial. However, increasing the key dim does add more dense parameters to
the model, and thus we cannot increase it indefinitely without breaking our fair comparisons. We pick a key
dimension of half the base model dim for our experiments.
```
**번역**:  
이 실험 결과는 표 4 왼쪽에 제시했으며, 기본 설정이 최적임을 확인했다. 표 4 오른쪽에서는 키 임베딩 차원을 독립적으로 늘리는 경우를 실험했다. 키 차원을 늘리면 성능이 좋아지는 것은 당연했다. 하지만 키 차원을 늘리면 모델에 더 많은 밀집 파라미터가 추가되므로, 공정한 비교를 위해 무한정 늘릴 수는 없다. 우리는 실험에서 키 차원을 베이스 모델 차원의 절반으로 선택했다.

```
nll NQnll TQAnll
v_dim #values
64 16m 2.15 12.86 8.75
256 4m 2.14 12.63 8.49
1024 1m 2.11 12.13 8.34
2048 512k 2.14 12.49 8.53
```
**번역(표 4 왼쪽)**:  
- value 차원을 바꾸면서 #values(값 개수)도 바꿔 전체 파라미터는 동일하게 유지  
  - 예) v_dim=64, 값 1600만 개(16m) → NQ nll=12.86, TQA nll=8.75  
  - v_dim=1024, 값 100만 개(1m) → 성능이 상대적으로 좋음

```
nll NQnll TQAnll
key_dim
256 2.11 12.13 8.34
512 2.12 12.32 8.15
1024 2.11 12.37 8.25
2048 2.09 11.98 7.83
```
**번역(표 4 오른쪽)**:  
- key_dim을 늘릴 때의 nll 변화  
  - key_dim=2048이면 NQ nll=11.98, TQA nll=7.83으로 가장 좋음

```
Table4Ablationstudies: ontheleft,varyingthevalueembeddingdimwhilekeepingtotalparametercountthesame,
ontherightvaryingkeydim.Metricsareallloglikelihood,onthetrainingset,NQanswersandTQAanswers.These
wereranonthe373mmodelsize,whichusesalatentdimensionof1024.key_dimisthesumofthedimensionofthe
sub-keys.
```
**번역**:  
표 4: 왼쪽은 전체 파라미터 수를 동일하게 유지하면서 value 임베딩 차원을 바꾸는 실험, 오른쪽은 key 차원을 바꾸는 실험이다. 모든 지표는 학습 세트, NQ 답변, TQA 답변 각각의 로그우도다. 이 실험은 잠재 차원이 1024인 3억7천3백만(373m) 모델 크기에서 실행되었다. key_dim은 서브 키(sub-keys)의 차원 합이다.

---

### 6 Implicationsandshortcomingsofthework

```
Scaling of dense transformer models has dominated progress in the AI field in the last 6 years. As this scaling
is nearing its physical and resource limits, it’s useful to consider alternatives which might be equally scalable
without being as compute and energy intensive. Memory layers with their sparse activations nicely complement
dense networks, providing increased capacity for knowledge acquisition while being light on compute. They
can be efficiently scaled, and provide practitioners with an attractive new direction to trade-off memory with
compute.
```
**번역**:  
지난 6년간 AI 분야의 발전은 밀집 트랜스포머 모델을 확장하는 데 주로 의존해 왔다. 하지만 이제 이러한 확장이 물리적·자원적 한계에 가까워짐에 따라, 동등한 수준으로 확장 가능하면서도 계산·에너지를 그만큼 많이 소모하지 않는 대안을 고려하는 것이 유용해졌다. 희소 활성화를 사용하는 메모리 레이어는 밀집 네트워크를 잘 보완하여, 계산량이 적으면서도 지식 습득 용량을 늘릴 수 있다. 또한 효율적으로 확장 가능하며, 실무자들에게 메모리와 계산량의 절충점을 모색하는 매력적인 새 방향을 제시한다.

```
While the memory layer implementation presented here is orders of magnitude more scalable than previous
works, there still remains a substantial engineering task to make them efficient enough for large scale production
uses. Dense architectures have been optimized for and co-evolved with modern GPU architectures for decades.
While we believe it’s in principle possible to make memory layers as fast, or even faster than regular FFN
layers on current hardware, we acknowledge that this needs non-trivial effort.
```
**번역**:  
본 연구에서 제시한 메모리 레이어 구현이 이전 연구보다 훨씬 확장성이 뛰어나지만, 이를 대규모 생산 환경에서 충분히 효율적으로 만들기 위해서는 여전히 상당한 엔지니어링 과제가 남아 있다. 밀집 아키텍처는 수십 년 동안 현대 GPU 아키텍처와 함께 최적화 및 공동 발전을 거듭해 왔다. 우리는 현재 하드웨어에서도 메모리 레이어를 일반 FFN 레이어만큼 혹은 더 빠르게 만들 수 있다고 원칙적으로 믿지만, 이에는 만만치 않은 노력이 필요함을 인정한다.

```
We have so far presented only high level empirical evidence that memory layers improve factuality of models.
However, we believe the sparse updates made possible by memory layers might have deep implications to how
models learn and store information. In particular, we hope that new learning methods can be developed to
push the effectiveness of these layers even further, enabling less forgetting, fewer hallucinations, and continual
learning.
```
**번역**:  
지금까지 우리는 메모리 레이어가 모델의 사실성을 개선한다는 높은 수준의 실증적 증거만 제시했다. 하지만 우리는 메모리 레이어가 가능하게 하는 희소적 업데이트(sparse updates)가, 모델이 정보를 학습하고 저장하는 방식에 대해 깊은 함의를 지닐 수 있다고 믿는다. 특히 새로운 학습 기법을 개발해 이러한 레이어의 효율을 더욱 끌어올린다면, 망각을 줄이고 환각을 억제하며 연속 학습(continual learning)을 구현할 수도 있기를 바란다.

```
Acknowledgments
We would like to thank Francisco Massa, Luca Wehrstedt for valuable input on making memory layers
more efficient; Gabriel Synnaeve, Ammer Rizvi, Michel Meyer for helping to provide resources for scaling
experiments.
```
**번역(감사의 말)**:  
**감사의 말**: 우리는 메모리 레이어를 더 효율적으로 만드는 데 유용한 의견을 준 Francisco Massa, Luca Wehrstedt에게 감사드린다. 그리고 확장 실험에 필요한 리소스를 제공해준 Gabriel Synnaeve, Ammer Rizvi, Michel Meyer에게도 감사를 표한다.

---

### (이하 참고문헌 부분)

생략
