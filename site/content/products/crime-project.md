---
title: "데이터를 통한 범죄발생예측"
draft: false
featured: true
weight: 1
description: 장소·시간대·요일 정보로 범죄 다발 여부를 예측하고, 결과를 바탕으로 범죄 예방 전략을 제안한 데이터 분석 프로젝트
---

<div class="pj-page">

<!-- ===== 프로젝트 개요 ===== -->
<div class="pj-meta">
  <div class="pj-meta-item">
    <span class="pj-meta-label">진행 시기</span>
    <span class="pj-meta-value">2024.09 ~ 2024.12</span>
  </div>
  <div class="pj-meta-item">
    <span class="pj-meta-label">진행 상태</span>
    <span class="pj-meta-value"><span class="pj-status">완료</span></span>
  </div>
  <div class="pj-meta-item">
    <span class="pj-meta-label">진행 인원</span>
    <span class="pj-meta-value">3인</span>
  </div>
</div>

<!-- ===== 1. 활동 목적 ===== -->
<h2 class="pj-section-title">활동 목적</h2>

<p class="pj-text">
  경찰 자원은 한정되어 있으므로 범죄가 언제, 어디서, 어떤 유형으로 집중되는지를 데이터로 파악하면 순찰과 자원 배치를 더 효율적으로 할 수 있다고 보았다.
  이에 따라 장소·시간대·요일 정보로 범죄 다발 여부를 예측하는 모델을 만들고 그 결과를 바탕으로 범죄 예방 전략을 제안하는 것을 목표로 한다.
</p>


<!-- ===== 2. 역할 및 기여 ===== -->
<h2 class="pj-section-title">역할 및 기여</h2>

<div class="pj-roles">
  <div class="pj-role">
    <p class="pj-role-title">공동 작업</p>
    <ul class="pj-list">
      <li>주제 선정</li>
      <li>KOSIS 데이터 수집</li>
      <li>모델 결과 해석</li>
      <li>결론 및 예방 전략 도출</li>
    </ul>
  </div>
  <div class="pj-role pj-role-me">
    <p class="pj-role-title">나의 역할</p>
    <ul class="pj-list">
      <li><strong>전처리</strong>: 데이터 구조 변경, 변수명 정리, 이상치 제거, 로그 변환</li>
      <li><strong>모델링</strong>: 로지스틱 회귀</li>
    </ul>
  </div>
</div>

<!-- ===== 3. 전체 수행 단계 ===== -->
<h2 class="pj-section-title">전체 수행 단계</h2>

<ol class="pj-flow">
  <li><span class="pj-flow-step">데이터 수집</span><span class="pj-flow-desc">KOSIS</span></li>
  <li><span class="pj-flow-step">데이터 전처리</span><span class="pj-flow-desc">구조 변경 · 이상치 처리</span></li>
  <li><span class="pj-flow-step">모델링</span><span class="pj-flow-desc">로지스틱 회귀 · 의사결정나무</span></li>
  <li><span class="pj-flow-step">성능 평가</span><span class="pj-flow-desc">교차검증 · ROC</span></li>
  <li><span class="pj-flow-step">예방 전략 도출</span><span class="pj-flow-desc">결과 기반 제안</span></li>
</ol>


<!-- ===== 4. 전처리 단계 ===== -->
<h2 class="pj-section-title">전처리 단계</h2>

<ol class="pj-steps">
  <li><strong>장소 변수 선별</strong>: 28개 장소 중 범죄 합계 상위 10개만 남김</li>
  <li><strong>데이터 구조 변경</strong>: 시간대·장소·요일을 각각 하나의 열로 재구성</li>
  <li><strong>변수명 정리</strong>: 가독성을 높이고 인코딩 오류를 막기 위해 영문화</li>
  <li><strong>로그 변환</strong>: 한쪽으로 치우친 분포 완화</li>
  <li><strong>이상치 처리</strong>: IQR 기준으로 탐지 후 중앙값으로 대체</li>
  <li><strong>다중공선성 확인</strong>: VIF로 독립변수 간 상관관계 점검</li>
  <li><strong>데이터 분할</strong>: 훈련 80 : 테스트 20</li>
</ol>

<div class="pj-callout">
  <p class="pj-callout-title">이상치 처리 방식 선택 이유</p>
  <ul class="pj-list">
    <li>박스플롯을 그려 보니 시간대·요일·장소별로 극단값이 많음을 확인</li>
    <li>일반적인 방법처럼 이상치를 삭제하면 특정 장소나 시간대에 범죄가 몰린다는 의미 있는 정보까지 사라질 가능성 존재</li>
    <li>그래서 IQR 기준(<code>Q1 − 1.5×IQR</code> 미만, <code>Q3 + 1.5×IQR</code> 초과)으로 이상치를 찾되 <strong>행은 남기고 값만 중앙값으로 대체</strong>하는 함수를 작성</li>
    <li>평균은 이상치에 끌려가므로 중앙값을 선택</li>
  </ul>
</div>

<!-- ===== 5. 산출물 및 결과 ===== -->
<h2 class="pj-section-title">산출물 및 결과</h2>

<!-- 5-1. 전처리 -->
<div class="pj-output">
  <p class="pj-output-title"><span class="pj-output-num">01</span>전처리</p>

  <figure class="pj-figure">
    <img src="/img/project/crime/log-transform.png" alt="로그 변환 전후 분포 비교">
    <figcaption>로그 변환 전후 분포</figcaption>
  </figure>
  <p class="pj-result">
    범죄 건수 분포가 한쪽으로 크게 치우쳐 있어 로그 변환을 적용한 결과 변환 후 분포의 치우침이 완화되었다.
  </p>

  <div class="pj-figure-row">
    <figure class="pj-figure">
      <img src="/img/project/crime/boxplot.png" alt="이상치 처리 전/후 박스플롯">
      <figcaption>이상치 처리 전/후</figcaption>
    </figure>
  </div>
  <p class="pj-result">
    처리 전에는 시간대·요일·장소별로 극단값이 많이 나타났지만 IQR 기준으로 찾은 이상치를 중앙값으로 대체한 뒤에는 행을 삭제하지 않고도 극단값이 줄어든 것을 확인하였다.
</div>

<!-- 5-2. 모델링 -->
<div class="pj-output">
  <p class="pj-output-title"><span class="pj-output-num">02</span>모델링</p>

  <figure class="pj-figure">
    <img src="/img/project/crime/model-compare.png" alt="로지스틱 회귀와 의사결정나무 성능 비교">
    <figcaption>로지스틱 회귀 vs 의사결정나무 성능 비교</figcaption>
  </figure>
  <p class="pj-result">
    로지스틱 회귀와 의사결정나무 두 모델을 교차검증과 ROC 곡선으로 비교한 결과 로지스틱 회귀 모델의 MSE가 더 낮아 로지스틱 회귀 모델 채택하였다.
  </p>
</div>

<!-- 5-3. 결론 -->
<div class="pj-output">
  <p class="pj-output-title"><span class="pj-output-num">03</span>결론</p>

  <p class="pj-sub">분석 결과</p>
  <div class="pj-findings">
    <div class="pj-finding">
      <p class="pj-finding-title">요일별 범죄 발생</p>
      <p class="pj-text">
        범죄 발생은 주로 주말에 집중되어, 토요일과 일요일에 나이트클럽, 펍, 주요 도로 등에서 기타범죄, 지능범죄, 폭력범죄가 많이 발생한 걸 확인할 수 있다.
      </p>
    </div>
    <div class="pj-finding">
      <p class="pj-finding-title">장소별 범죄 발생</p>
      <p class="pj-text">
        도로(MAINROAD), 나이트클럽(NIGHT CLUB), 펍(PUB), 레스토랑(RESTAURANT) 등에서는 시간대별로 범죄 발생 확률이 높았음을 확인 할 수 있다.
      </p>
    </div>
    <div class="pj-finding">
      <p class="pj-finding-title">시간대별 범죄 발생</p>
      <p class="pj-text">
        DAWN, MORNING처럼 범죄가 적은 시간대 자체보다는 주요 장소와 특정 범죄 유형이 범죄 발생에 더 큰 영향을 미쳤으며 주로 주말 시간의 영향을 많이 받았음을 확인할 수 있다.
      </p>
    </div>
  </div>

  <p class="pj-sub">범죄 예방 전략</p>
  <ol class="pj-steps">
    <li><strong>주말 집중 순찰</strong>: 범죄가 몰리는 토요일·일요일에 나이트클럽, 펍이 밀집한 지역과 주요 도로를 중심으로 순찰 인력을 늘린다.</li>
    <li><strong>고위험 장소 맞춤 관리</strong>: 도로, 나이트클럽, 펍, 레스토랑 주변에 CCTV와 조명을 확충하고 업소와 협력해 영업 시간대 안전 관리를 강화한다.</li>
    <li><strong>범죄 유형별 대응</strong>: 폭력범죄는 주점가 주변 신속 출동 체계를 갖추고 지능범죄는 사기 수법 안내 등 예방 홍보를 함께 진행한다.</li>
    <li><strong>경찰 자원 재배치</strong>: 범죄가 적은 새벽·아침 시간대의 인력을 주말과 고위험 장소로 옮겨 한정된 자원을 효율적으로 활용한다.</li>
  </ol>
</div>









