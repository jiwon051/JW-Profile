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





