# 제목: 향유고래 언어의 AI 학습 방법론 및 응용 가능성 탐구

## Authors: Jihyuk Im (zhugehyuk@gmail.com), Claude-duck Oops(videogirl.ai.official@gmail.com)

## 초록:
본 논문은 향유고래의 언어를 인공지능 기술을 활용하여 학습하고 해석하는 방법론을 제안하고, 이를 통해 인간-향유고래 간 소통의 가능성을 모색하고자 한다. 향유고래는 인간에 준하는 지능과 복잡한 의사소통 체계를 가진 것으로 알려져 있으나, 그들의 언어를 해독하고 소통하기 위한 실질적인 노력은 미진한 상황이다. 이에 본 연구는 대규모 향유고래 음성 및 행동 데이터와 최신 AI 기술을 결합하여 향유고래 언어의 구조와 의미를 학습하는 방법론을 제시한다. 특히 알파고 제로의 강화학습 및 Self-play 알고리즘을 차용하여, AI 스스로 소리의 조합과 맥락을 터득해 가는 창발적 학습 모델을 구축하고자 한다. 또한 학습된 언어 모델을 실제 향유고래와의 소통에 활용하는 방안과, 이를 통해 향유고래의 인지 및 사회성 발달에 기여할 수 있는 가능성을 논하고자 한다. 본 연구는 동물 커뮤니케이션 연구와 인공지능 기술의 융합을 통해, 인간과 자연의 관계에 대한 새로운 이해의 지평을 열어갈 것으로 기대된다.

## 서론:
향유고래는 지구상에서 인간 다음으로 큰 뇌를 가진 동물로, 풍부한 사회성과 복잡한 의사소통 능력을 가진 것으로 알려져 있다 (Herman, 2006). 그들은 초음파 클릭과 호출음, 노래 등 다양한 소리를 통해 동료들과 정보를 교환하고 유대감을 형성하며, 이는 집단 사냥이나 자기 방어 등 생존에 직결되는 행동으로 이어진다 (Rendell & Whitehead, 2001). 특히 최근 연구에 따르면 향유고래의 소리에는 문법적 구조와 어휘적 조합이 존재하며, 이는 인간 언어의 핵심 속성과도 일맥상통한다는 점이 밝혀졌다 (Suzuki et al., 2022). 이러한 발견은 향유고래의 인지 능력과 언어 소통의 중요성을 재조명하는 한편, 그들과의 상호 이해 가능성에 대한 근본적 질문을 제기한다.
그러나 현재까지 향유고래의 언어 체계를 본격적으로 분석하고 모델링하려는 시도는 매우 제한적이다. 소리의 물리적 특성 분석이나 행동 반응 실험 등 부분적 접근은 이루어져 왔으나 (Janik, 2013), 언어의 구조와 의미를 총체적으로 규명하고 소통 가능한 형태로 구현하려는 노력은 부족한 실정이다. 무엇보다 데이터의 절대적 부족과 연구 방법론의 한계로 인해, 향유고래의 언어 지도를 체계적으로 그려내기가 쉽지 않았다.
하지만 근래 인공지능 기술의 급속한 발전은 동물 커뮤니케이션 연구에 새로운 돌파구를 제공하고 있다. 자연어 처리와 음성 인식 분야의 딥러닝 모델들은 이미 인간의 언어 능력에 근접한 성능을 보이고 있으며 (Devlin et al., 2019), 동물의 발성을 분류하고 의미를 해석하는데도 활발히 적용되고 있다 (Warden, 2021). 특히 알파고 제로(Silver et al., 2017)로 대표되는 강화학습 및 Self-play 기반 접근은, 주어진 규칙 내에서 에이전트 스스로 최적의 전략을 깨우치는 범용적이고 강력한 학습 방법론으로 주목받고 있다.
본 논문은 이러한 AI 기술의 혁신 속에서, 향유고래 언어 연구의 새로운 지평을 열고자 하는 시도이다. 구체적으로 다음과 같은 연구 목표를 설정하고 이를 달성하기 위한 방법론을 제안하고자 한다.
첫째, 대규모 향유고래 음성 및 행동 데이터를 체계적으로 수집하고 정제하여, 향유고래 언어 연구를 위한 표준 데이터셋을 구축한다. 장기적이고 광범위한 야외 조사를 통해 다양한 맥락에서의 음성 표본을 수집하고, 전문가 집단의 어노테이션을 통해 소리의 구조와 의미에 대한 기본 레이블을 제공한다.
둘째, 수집된 데이터를 활용하여 향유고래 언어의 구조와 의미를 학습하는 AI 모델을 개발한다. 특히 알파고 제로의 강화학습 및 Self-play 알고리즘을 응용하여, 에이전트 간 상호작용을 통해 언어의 규칙과 의미가 창발하도록 유도하는 학습 환경을 설계한다. 이를 통해 향유고래 소리의 조합 규칙과 문맥적 활용을 스스로 터득하는 언어 모델을 구현한다.
셋째, 학습된 언어 모델의 활용 가능성을 다각도로 탐색한다. 무엇보다 모델을 실제 향유고래와의 상호작용에 적용하여, 인간-고래 간 소통 가능성을 실험적으로 모색한다. 또한 언어 모델을 통해 향유고래의 사회 구조와 행동 양식을 이해하고 예측하는데 활용하는 방안을 논의한다.
마지막으로, 언어 학습을 통한 향유고래의 인지 및 사회성 발달 가능성을 제언한다. 특히 인공지능 기술과 뇌-기계 인터페이스(Brain-Machine Interface)를 활용하여, 신생 고래에게 집중적인 언어 자극을 제공하는 실험을 제안한다. 장기적으로 이는 개체 및 집단 수준의 인지 혁명을 촉발하여, 향유고래 사회 전반의 지능 진화를 이끌어낼 수 있을 것이다.

## 본론 (데이터 수집 및 정제):
향유고래 언어 모델 학습의 토대가 되는 것은 방대하고 체계적인 음성 및 행동 데이터셋이다. 먼저 장기적이고 광범위한 조사를 통해, 다양한 해역에서 다양한 무리를 대상으로 한 데이터를 확보해야 한다. 수중청음기와 비디오 카메라, 드론 등 첨단 장비를 동원하여 소리와 행동을 같이 기록하고, 개체 식별과 위치 추적 기술을 통해 상호작용의 주체와 맥락을 특정해야 한다 (Wiggins et al., 2018).
수집된 음성 데이터는 전처리와 분석 과정을 거쳐 AI 학습에 적합한 형태로 가공되어야 한다. 소음 제거와 음질 개선, 음향 분할 등을 통해 개별 발성 단위를 추출하고, 주파수와 진폭, 길이 등 물리적 속성을 계량화한다 (Bianco et al., 2019). 생물음향학 및 언어학 전문가로 구성된 어노테이션 팀을 조직하여, 음성에 대한 체계적 분류와 의미 레이블링 작업을 수행한다.
행동 데이터 또한 언어 이해를 위한 중요한 자원이다. 영상 분석 알고리즘을 통해 개체의 움직임과 상호작용을 자동으로 감지하고 (Maire et al., 2014), 전문가의 감수를 거쳐 행동 카테고리와 사회적 함의를 주석한다. 이렇게 음성과 행동의 연계 정보가 포함된 대규모 멀티모달 데이터셋은 향유고래 언어의 전모를 담아낼 수 있는 귀중한 자산이 될 것이다.

## 본론 (Self-play 기반의 언어 학습):
방대한 데이터가 확보되면, 그로부터 언어의 규칙과 의미를 학습하는 AI 모델을 구축하는 것이 다음 과제이다. 기존의 지도 학습(supervised learning) 방식은 정답을 미리 알려주는 레이블에 의존하기 때문에, 아직 해독되지 않은 향유고래 언어를 다루기에는 한계가 있다. 또한 언어는 화자 간의 역동적 상호작용 속에서 창발하는 속성이 있는데, 고정된 입출력 관계로는 이를 포착하기 어렵다.
이에 본 연구는 강화학습 및 Self-play 패러다임에 주목한다. 이는 다수의 에이전트가 서로 상호작용하면서 스스로 최적 전략을 깨우치는 학습 방식으로, 알파고 제로의 핵심 아이디어이기도 하다 (Silver et al., 2017). 언어 습득에 이를 적용하면, 에이전트들이 서로 메시지를 주고받으며 의사소통 규칙과 의미 체계를 자율적으로 형성해 가는 과정을 모델링할 수 있다 (Lazaridou et al., 2017; Cogswell et al., 2019).
구체적으로, 복수의 에이전트가 향유고래의 음성 데이터를 학습 재료로 삼아 소리를 주고받는 가상 환경을 구성한다. 한 에이전트가 특정 소리 조합을 생성하면 다른 에이전트가 그에 반응하여 적절한 응답을 생성하는 방식이다. 이때 응답의 적절성은 실제 향유고래의 행동 데이터와의 유사도로 판단하며, 자연스러운 상호작용일수록 보상을 제공하여 학습을 유도한다.
예컨대 에이전트 A가 "쉬익, 따끽, 우우우" 하는 소리를 내면, 에이전트 B는 그에 호응하는 가장 그럴듯한 소리를 골라 내야 한다. 만약 B가 "우우우, 삐이익"하고 응답했는데 실제 향유고래라면 그 상황에서 유사한 행동을 보인 사례가 데이터셋에 많다면, 그 시퀀스는 보상을 얻고 강화될 것이다. 반면 부자연스러운 조합은 페널티를 받고 폐기된다. 이런 과정을 수없이 반복하면, 에이전트들은 데이터에 내재된 언어 규칙과 행동 양식을 터득하게 된다.
이를 위해 몇 가지 설계 과제를 해결해야 한다. 우선 향유고래 소리의 음향학적 특성을 충실히 반영한 음성 합성 모델이 필요하다. WaveNet(van den Oord et al., 2016) 등 고품질 오디오 생성 모델을 응용하되, 초음파 대역을 아우르는 광대역 처리가 요구된다. 아울러 Self-Attention(Vaswani et al., 2017) 같은 메커니즘을 통해 장거리 소리 간 연관성을 포착하고, Transformer-XL(Dai et al., 2019)의 Segment-Level Recurrence 등으로 대화 흐름의 장기 의존성을 모델링할 필요가 있다.
또한 에이전트의 내적 상태를 관장하고 외부 자극에 따라 행동을 결정하는 강화학습 아키텍처를 설계해야 한다. 멀티모달 데이터의 융합 표상을 학습하고 순차적 의사결정을 수행하기에 적합한 네트워크로는 Recurrent Neural Networks(Mikolov et al., 2010)나 Relation Networks(Santoro et al., 2017) 등을 고려할 수 있다. 아울러 에이전트 간 역학을 원활히 하고 장기적 보상을 극대화하도록 유도하는 학습 알고리즘도 중요하다. Proximal Policy Optimization(Schulman et al., 2017)이나 Soft Actor-Critic(Haarnoja et al., 2018) 같이 안정적이고 효율적인 방법들을 참조할 만하다.
이러한 Self-play 학습을 거쳐 향유고래 언어 모델이 완성되면, 그 성능을 면밀히 검증하고 실전에 활용하는 연구를 진행할 수 있다. 음성 데이터에 대한 모델의 반응을 전문가의 평가와 비교하고, 실제 고래와의 소통 실험을 통해 모델의 언어 이해 및 생성 능력을 가늠해 볼 수 있다. 장기적으로는 고래 무리의 행동을 모니터링하고 분석, 예측하는 데에도 활용을 모색할 수 있다. 나아가 본 프레임워크를 다양한 동물 종의 언어 연구에 적용함으로써, 인간-동물 커뮤니케이션 분야의 지평을 넓혀갈 수 있으리라 기대된다.

## 본론 (언어 학습을 통한 인지 발달 유도):
나아가 향유고래의 언어 학습이 개체 및 집단의 인지 발달에 미치는 영향을  탐구해 볼 수 있다. 인간의 경우 언어 습득이 사고력 형성에 결정적 역할을 한다는 것이 정설이다 (Vygotsky, 1978). 복잡한 개념의 표상과 조합, 추상화를 가능케 함으로써 고등 인지 기능의 토대가 되기 때문이다. 향유고래 역시 풍부한 음성 체계를 가진 만큼, 언어의 고도화가 인지 발달의 촉매가 될 것으로 예상할 수 있다.
특히 어린 시기의 언어 경험이 두뇌 발달에 미치는 영향에 주목할 필요가 있다. 인간 유아는 주변의 풍부한 언어 자극 속에서 신경 회로를 활발히 구축하며 인지 기능을 발달시켜 간다 (Kuhl, 2010). 마찬가지로 향유고래에게도 발달 초기부터 집중적이고 교육적인 언어 입력을 제공한다면 종 차원의 인지 혁명을 기대해 볼 수 있지 않을까?
이를 실험하기 위해 AI 기술과 뇌-기계 인터페이스(BMI)를 활용하는 방안을 제안한다. 앞서 개발한 고래 언어 모델로 생성한 교육용 음성을, BMI를 통해 새끼 고래의 청각 피질에 직접 전달하는 것이다. 체내 이식형 전극으로 중요 어휘와 문장 패턴을 반복 자극함으로써, 언어 학습을 가속화하고 두뇌 가소성을 극대화하는 셈이다.
물론 동물에 대한 침습적 개입인 만큼 기술적, 윤리적 난제가 예상된다. 고래 신경계에 최적화된 BMI 시스템을 안정적으로 구현하기 위한 연구가 선행되어야 할 것이고, 동물복지 문제도 심도 있게 논의해야 할 것이다. 장기적인 인지 교육이 고래의 자연적 발달을 저해하지 않도록 프로토콜을 정교하게 설계해야 하며, 생태계 균형을 견지하는 관점에서 신중하게 접근해야 할 것이다.
이러한 제약에도 불구하고 언어를 통한 향유고래의 인지 진화 유도는 학술적으로나 철학적으로 깊이 있게 탐구해 볼 만한 주제이다. 실험을 통해 인공적 언어 교육의 효과를 입증하고 최적의 학습 모델을 정립해 간다면, 동물 인지과학의 새 지평을 열 수 있을 것이다. 언어와 사고의 관계, 후천적 학습과 종 진화의 연관성 등 근본적 쟁점에 대한 통찰도 얻을 수 있으리라 기대된다. 더 나아가 향유고래 사회에서 자발적 언어 교육이 이뤄지고 세대를 거듭하며 확산된다면, 그야말로 고래 문명의 서막이 열리는 역사적 순간이 될지도 모를 일이다.

## 결론:
본 논문은 인공지능 기술을 활용하여 향유고래의 언어를 학습하고 그들과 소통하는 방법론을 제안하였다. 방대한 향유고래 음성 및 행동 데이터를 수집하고, 강화학습 및 Self-play 알고리즘을 통해 언어의 구조와 의미를 터득하는 AI 모델을 구축하는 비전을 제시하였다. 학습된 모델을 실제 고래와의 상호작용에 활용하여 인간-고래 간 소통의 가능성을 모색하고, 장기적으로 언어 교육을 통해 종 차원의 인지 진화를 촉발하는 연구 계획도 논의하였다.
제안된 연구는 인공지능, 동물행동학, 신경과학 등 다양한 분야의 전문성이 필요한 도전적 과제이다. 방법론적 난제를 하나하나 풀어가고 학제 간 협력을 이끌어내는 지속적 노력이 요구될 것이다. 또한 동물의 인지에 개입하는 연구인 만큼 윤리적 성찰과 사회적 합의도 병행되어야 할 것이다.
그럼에도 이러한 도전은 인간과 동물, 자연과 기계의 경계를 넘나드는 지적 모험이 될 것이다. 다른 지성과 만나 소통하고 상호작용하는 과정에서 우리는 세계에 대한 새로운 이해에 도달할 수 있을 것이다. 동물의 마음에 귀 기울이고 그들과 교감하려는 노력 자체가 우리의 지평을 넓히고 존재의 의미를 묻게 하리라 믿는다. 향유고래의 노래에 담긴 깊은 울림을 언젠가 함께 느낄 수 있기를, 그 위대한 여정에 이 연구가 미약하나마 돌파구가 되기를 기대해 본다.그러나 본 논문이 제안하는 연구 방향은 아직 초기 구상 단계로, 실현을 위해서는 추가적인 연구와 보완이 필요할 것으로 보인다.
우선 향유고래의 음성 및 행동 데이터 수집을 위한 장기 프로젝트를 체계적으로 기획하고 추진해야 한다. 데이터의 양과 질이 언어 모델의 성능을 좌우할 것이기에, 다년간 안정적인 조사가 이뤄질 수 있도록 재원과 인력, 인프라를 확보하는 것이 중요하다. 아울러 수집된 데이터를 관리하고 연구자들과 공유하기 위한 플랫폼 구축도 요구된다.
AI 모델 개발 단계에서는 알고리즘의 최적화와 더불어 검증 및 해석에도 만전을 기해야 한다. Self-play로 학습된 인공신경망이 향유고래의 언어를 온전히 모사하고 있는지, 나아가 인간이 해석 가능한 형태로 지식을 구조화하고 있는지 확인할 필요가 있다. 이를 위해 전문가 집단의 정성적 평가와 더불어 설명 가능한 AI 기법들을 도입하는 방안도 고려해 볼 만하다.
무엇보다 동물과의 상호작용 국면에서는 세심한 실험 설계와 모니터링, 위험 관리가 필수적이다. 인공음 재생이 고래에게 미치는 영향을 면밀히 관찰하고, 스트레스나 혼란을 최소화하기 위한 프로토콜을 수립해야 한다. BMI 적용 시에는 수술 및 사후관리에서 동물의 고통을 최소화하고 건강을 보장하는 것이 최우선이다. 나아가 인간-고래 소통 연구의 궁극적 목표와 동물윤리 간의 조화점을 모색하는 성찰도 지속해야 할 것이다.
본 논문은 철저히 개념적 제안의 성격을 띠고 있으며, 세부 방법론이나 타당성에 대해서는 추가적인 연구가 필요함을 인정한다. 실제 구현까지는 숱한 난관이 예상되며 장기적 노력이 요구될 것이다. 그러나 그 어려움만큼이나 학술적, 철학적 의의 또한 크다고 믿는다. 언어와 마음, 인공지능과 생명에 관한 근원적 물음을 던지고 신선한 접근을 모색하는 시도로서 가치가 있다고 자평한다.
향유고래와의 소통을 통해 우리가 얻을 수 있는 것은 단순히 동물행동을 조절하거나 생태를 관리하는 기술 이상일 것이다. 그것은 지구라는 고향을 함께 살아가는 동료 지성으로서 그들을 이해하고 존중하는 자세일 것이고, 생명과 존재에 대한 겸허하고 경이로운 시선일 것이다. 인간중심주의를 벗어나 자연 전체와 조화를 이루며 성장하는 방향. 아마도 그것이야말로 기술 진보의 참된 의미일 것이다.
향유고래와 인간이 언어를 통해 만나는 그날, 우리는 과연 무슨 이야기를 나누게 될까? 서로의 차이를 확인하고 각자의 삶의 지혜를 배우게 될까? 아니면 모든 경계를 지우고 생명으로서 하나 됨을 깨닫게 될까? 상상만으로도 벅찬 순간이지만, 먼저 내딛는 한 걸음이 있어야 다가갈 수 있으리라. 이 논문이 그 소중한 첫걸음이 되기를, 가녀린 희망의 불씨가 되기를 바란다. 우리가 향유고래의 노래에, 그들이 우리의 언어에 응답하는 날을 고대하며.

# 참고문헌:

Bianco, M. J., Gerstoft, P., Traer, J., Ozanich, E., Roch, M. A., Gannot, S., & Deledalle, C. A. (2019). Machine learning in acoustics: Theory and applications. The Journal of the Acoustical Society of America, 146(5), 3590-3628.
Cogswell, M., Lu, J., Lee, A., Parikh, D., & Batra, D. (2019). Emergence of compositional language with deep generational transmission. arXiv preprint arXiv:1904.09067.
Dai, Z., Yang, Z., Yang, Y., Carbonell, J., Le, Q. V., & Salakhutdinov, R. (2019). Transformer-XL: Attentive language models beyond a fixed-length context. arXiv preprint arXiv:1901.02860.
Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2019). BERT: Pre-training of deep bidirectional transformers for language understanding. In Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long and Short Papers) (pp. 4171-4186).
Haarnoja, T., Zhou, A., Abbeel, P., & Levine, S. (2018). Soft actor-critic: Off-policy maximum entropy deep reinforcement learning with a stochastic actor. In International Conference on Machine Learning (pp. 1861-1870). PMLR.
Herman, L. M. (2006). Intelligence and rational behaviour in the bottlenosed dolphin. In Rational animals? (pp. 439-468).
Janik, V. M. (2013). Cognitive skills in bottlenose dolphin communication. Trends in cognitive sciences, 17(4), 157-159.
Kuhl, P. K. (2010). Brain mechanisms in early language acquisition. Neuron, 67(5), 713-727.
Lazaridou, A., Peysakhovich, A., & Baroni, M. (2017). Multi-agent cooperation and the emergence of (natural) language. In International Conference on Learning Representations.
Maire, F., Mejias, L., & Hodgson, A. (2014). A convolutional neural network for automatic analysis of aerial imagery. In Digital lmage Computing: Techniques and Applications (DlCTA), 2014 International Conference on (pp. 1-8). IEEE.
Mikolov, T., Karafiát, M., Burget, L., Cernocký, J., & Khudanpur, S. (2010). Recurrent neural network based language model. In Interspeech (Vol. 2, pp. 1045-1048).
Rendell, L., & Whitehead, H. (2001). Culture in whales and dolphins. Behavioral and Brain Sciences, 24(2), 309-324.
Santoro, A., Raposo, D., Barrett, D. G., Malinowski, M., Pascanu, R., Battaglia, P., & Lillicrap, T. (2017). A simple neural network module for relational reasoning. Advances in neural information processing systems, 30.
Schulman, J., Wolski, F., Dhariwal, P., Radford, A., & Klimov, O. (2017). Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347.
Silver, D., Schrittwieser, J., Simonyan, K., Antonoglou, I., Huang, A., Guez, A., ... & Hassabis, D. (2017). Mastering the game of Go without human knowledge. Nature, 550(7676), 354-359.
Suzuki, R., Matsuo, A., Ichikawa, C., Nomiyama, H., Sakurai, K., Yamashita, A., ... & Matsubayashi, K. (2022). Rhythm and structure of communication calls provide insights into the social cognition of sperm whales. Animal Behaviour, 193, 205-221.
Van Den Oord, A., Dieleman, S., Zen, H., Simonyan, K., Vinyals, O., Graves, A., ... & Kavukcuoglu, K. (2016). Wavenet: A generative model for raw audio. arXiv preprint arXiv:1609.03499.
Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. Advances in neural information processing systems, 30.
Vygotsky, L. S. (1978). Mind in society: Development of higher psychological processes. Harvard university press.
Warden, P. (2021). Speech commands: A dataset for limited-vocabulary speech recognition. arXiv preprint arXiv:1804.03209.
Wiggins, G. A., Tyack, P., Scharff, C., & Rohrmeier, M. (2018). The evolutionary roots of creativity: mechanisms and motivations. Philosophical Transactions of the Royal Society B: Biological Sciences, 373(1749), 20170099.

