<template>
<h1>Stepper</h1>
  <!-- 
위에것 참고해서 진행표시 기능 넣기
   
  
  -->
  <!-- 
  <nav class="stepper" aria-label="진행 단계">
    <ol>
      <li :class="{ active: currentStep >= 1 }">
        <span class="dot" aria-hidden="true"></span>
        <span class="label">사물함 예약</span>
      </li>
      <li :class="{ active: currentStep >= 2 }">
        <span class="connector" aria-hidden="true"></span>
        <span class="dot" aria-hidden="true"></span>
        <span class="label">확인 및 결제</span>
      </li>
      <li :class="{ active: currentStep >= 3 }">
        <span class="connector" aria-hidden="true"></span>
        <span class="dot" aria-hidden="true"></span>
        <span class="label">완료 확인</span>
      </li>
    </ol>
  </nav> 
  -->
  <!-- =========추가===================== -->
  <!-- 상단 스텝 표시 -->
  <div class="stepper">
    <ol>
      <li class="step active">
        <div class="circle"></div>
        <p>예약 하기</p>
        <div class="dotline"></div>
      </li>
      <li class="step">
        <div class="circle"></div>
        <p>확인 및 결제</p>
        <div class="dotline"></div>
      </li>
      <li class="step">
        <div class="circle"></div>
        <p>변경 완료</p>
      </li>
    </ol>
  </div>
</template>

<script setup>
defineProps({ currentStep: { type: Number, default: 1 } });
</script>

<style lang="scss" scoped>
@use "/src/assets/style/variables" as *;

/* ✅ 기본 설정 */
.res-inner {
  width: 80%;
  margin: auto;
  background-color: antiquewhite;
  font-family: "Inter", "Pretendard", sans-serif;
  color: #333;
}

/* ✅ 상단 스텝 표시 */
.stepper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 4rem;
  margin: 3rem auto;
}

/* ✅ 순서 있는 목록 (ol) */
.stepper ol {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: clamp(2rem, 5vw, 5rem);
  list-style: none;
  padding: 0;
  margin: 0;
}

/* ✅ 각 단계 (step) */
.step {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  font-size: 16px;
  color: #bbb;
  font-weight: 400;
  text-align: center;

  /* ✅ 원(circle) */
  .circle {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 2px solid #bbb;
    background-color: #fff;
    margin-bottom: 0.5rem;
  }

  /* ✅ 점선(dotline) */
  .dotline {
    position: absolute;
    top: 50%; /* ✅ 원 중심 기준 */
    transform: translateY(-50%);
    right: -50%; /* ✅ 간격 자동 계산 */
    width: 100%;
    max-width: 90px;
    height: 2px;
    border-top: 2px dotted #bbb;
    z-index: 0;
  }

  /* ✅ 마지막 단계 뒤의 선 제거 */
  &:last-child .dotline {
    display: none;
  }

  /* ✅ 활성화 상태 (현재 단계) */
  &.active {
    color: #028587;
    font-weight: 600;

    .circle {
      border-color: $color_main_light;
      background-color: $color_main_deep;
    }

    .dotline {
      border-top-color: #9fd3cf;
    }
  }
}

/* ✅ 반응형 (모바일 세로형 Stepper) */
@media (max-width: 768px) {
  .stepper ol {
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
  }

  .step {
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 10px;
    text-align: left;

    /* ✅ 원 */
    .circle {
      margin-bottom: 0;
    }

    /* ✅ 점선 → 세로선 변경 */
    .dotline {
      top: 100%;
      left: 50%;
      transform: translateX(-50%);
      width: 2px;
      height: 40px;
      border-top: none;
      border-left: 2px dotted #bbb;
    }

    /* ✅ 마지막 점선 제거 */
    &:last-child .dotline {
      display: none;
    }
  }
}
</style>