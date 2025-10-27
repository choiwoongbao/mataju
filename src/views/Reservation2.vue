<template>
  <section class="reserve-page">
    <div class="inner">
      <Stepper :current-step="2" />

      <div class="wrap_reserv">

        <!-- 위쪽 2개 카드 (Grid 정렬) -->    
        <div class="reserve-container">
          <!-- 사물함 예약 카드 -->
          <div class="form_card line">
            <div class="card_header"><h3> 정보</h3></div>
            <div class="card_content">
              <table>
                <tbody>
                  <tr><td>성함</td><td>사물함 대여</td></tr>
                  <tr><td>휴대폰</td><td>사물함 대여</td></tr>
                  <tr><td>사물함사이즈</td><td>사물함 대여</td></tr>
                  <tr><td>대여장소</td><td>사물함 대여</td></tr>
                  <tr><td>예약날짜</td><td>사물함 대여</td></tr>
                  <tr><td>픽업장소</td><td>사물함 대여</td></tr>
                  <tr><td>배송지정일1</td><td>입력 필요</td></tr>
                  <tr><td>주소</td><td>입력 필요</td></tr>
                  <tr><td>상세주소</td><td>입력 필요</td></tr>
                  <tr><td>배송일2</td><td>입력 필요</td></tr>




                  <tr class="total"><td>총 결제금액</td><td><strong>29,000원</strong></td></tr>
                </tbody>
              </table>
            </div>
          </div>
          
          <!-- 선택 상품 요약 카드 -->
          <div class="summary_card line">
            <h2 class="card_title">선택 상품 요약</h2>
            <ul>
              <li v-for="tab in selectedTabs" :key="tab">
                {{ tab }} — {{ formatKrw(prices[tab]) }}
              </li>
    </ul>
    
    <div class="divider"></div>
    
    <div class="benefits">
      <h4>마일리지 / 쿠폰 사용</h4>
      <div class="benefit-row">
        <label class="inline">
          <input type="checkbox" v-model="useCoupon" />
          Welcome 쿠폰 - 3,000원
        </label>
        <span class="muted" v-if="useCoupon">- {{ formatKrw(3000) }}</span>
      </div>
      
      <div class="benefit-row">
        <label class="inline">
          <input type="checkbox" v-model="usePoints" />
          포인트 - 2,500P
        </label>
        <span class="muted" v-if="usePoints">- {{ formatKrw(2500) }}</span>
      </div>
    </div>
    
    <div class="total-row">
      <span>총 결제금액</span>
      <strong>{{ formatKrw(finalTotal) }}</strong>
    </div>
  </div>
</div>
<!-- 결제 카드 (아래에) -->
<div class="paysection">
  
  <div class="payment_card">
    <div class="card_header"><h3>결제방법 선택</h3></div>
    <div class="card_content">
      <div class="pay-grid" role="radiogroup">
        <button
        v-for="method in paymentMethods"
        :key="method.id"
        type="button"
        class="pay-card"
        :class="{ selected: selectedPayment === method.id }"
        @click="selectedPayment = method.id"
        >
        <span class="icon">{{ method.icon }}</span>
        <span class="label">{{ method.label }}</span>
      </button>
    </div>
  </div>
</div>
<button class="submit_btn" @click="saveAndPay">결제하기</button>
      </div>
    </div>
      
      
    </div>
  </section>
</template>


<script setup>
import { ref, computed } from "vue";
import Stepper from "@/components/reserv/Stepper.vue";

const selectedTabs = ref(["사물함 예약"]);
const useCoupon = ref(true);
const usePoints = ref(true);
const selectedPayment = ref("card");

const prices = {
  "사물함 예약": 29000,
  "짐 가져오기": 15000,
  "집으로 배송하기": 20000,
};

const totalPrice = computed(() =>
  selectedTabs.value.reduce((sum, tab) => sum + prices[tab], 0)
);

const discountAmount = computed(() => {
  let discount = 0;
  if (useCoupon.value) discount += 3000;
  if (usePoints.value) discount += 2500;
  return Math.min(discount, totalPrice.value);
});

const finalTotal = computed(() =>
  Math.max(totalPrice.value - discountAmount.value, 0)
);

const paymentMethods = [
  { id: "card", label: "신용카드", icon: "💳" },
  { id: "kakao", label: "카카오페이", icon: "💬 pay" },
  { id: "naver", label: "네이버페이", icon: "N pay" },
  { id: "bank", label: "무통장입금", icon: "🏦" },
];

const formatKrw = (v) =>
  new Intl.NumberFormat("ko-KR", { style: "currency", currency: "KRW" }).format(v);

const paymentLabel = computed(() => {
  const m = paymentMethods.find((p) => p.id === selectedPayment.value);
  return m ? m.label : "-";
});

const saveAndPay = () =>
  alert(`✅ 결제가 완료되었습니다!\n결제수단: ${paymentLabel.value}\n결제금액: ${formatKrw(finalTotal.value)}`);
</script>

<style lang="scss" scoped>
/* =========================================================
   💳 Reservation2 — rem & % 기반 정리 (vh / vw 완전 제거)
========================================================= */

/* ========== 1️⃣ 전면 레이아웃 ========== */
.reserve-page {
  background: #f5f7f7;
  min-height: 60rem; /* ✅ 100vh → 60rem (약 960px) */
  width: 100%; /* ✅ 100vw → 100% (스크롤바 문제 해결) */
  padding: 5rem 0; /* ✅ 80px → 5rem */
  position: relative;
  overflow-x: hidden; /* ✅ 뷰포트 기준 오프셋 방지 */
}

.inner {
  width: 90%;
  max-width: 87.5rem; /* ✅ 1400px → 87.5rem */
  margin: 0 auto;
}

/* ✅ 상단 레이아웃 구조 (flex → grid) */
.reserve-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2.5rem; /* ✅ 40px */
  align-items: start;
  justify-content: center;
  margin-bottom: 3.75rem; /* ✅ 60px */
  width: 100%;
  max-width: 87.5rem;
  margin-inline: auto;
}

/* =========================================================
   2️⃣ 카드 공통 스타일
========================================================= */
.form_card,
.summary_card,
.payment_card {
  background: #fff;
  border-radius: 0.625rem; /* 10px */
  box-shadow: 0 0.25rem 0.75rem rgba(0, 0, 0, 0.05);
  padding: 1.875rem 2.5rem; /* 30px 40px */
  border: 1px solid transparent;
  position: relative;
  transition: all 0.3s ease;

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 0.5rem; /* 8px */
    background: #53b4a1;
    border-top-left-radius: 0.625rem;
    border-top-right-radius: 0.625rem;
  }
}

/* Summary 카드 */
.summary_card {
  width: 25rem; /* 400px */

  .card_title {
    font-size: 1.125rem;
    font-weight: 600;
    color: #222;
    margin-bottom: 1.25rem;
  }

  ul {
    font-size: 0.875rem;
    color: #444;
    margin-bottom: 1.5rem;
  }
}

/* 결제 카드 */
.payment_card {
  width: 100%;
  max-width: 68.75rem; /* ✅ 1100px → 68.75rem */
  margin: 0 auto;

  .pay-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0.75rem; /* 12px */
    margin-bottom: 1.25rem;
  }

  .pay-card {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.625rem;
    padding: 1rem 0;
    border: 1px solid #ddd;
    border-radius: 0.5rem;
    background: #fff;
    cursor: pointer;
    transition: 0.3s;

    &:hover {
      border-color: #53b4a1;
    }

    &.selected {
      border-color: #53b4a1;
      background: #e9f8f8;
      color: #53b4a1;
      font-weight: 600;
    }

    .icon {
      font-size: 1.125rem;
    }
  }
}

.paysection {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* 버튼 */
.submit_btn {
  width: 70%;
  padding: 0.875rem 0;
  font-weight: 600;
  font-size: 0.9375rem;
  color: #fff;
  background: #53b4a1;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: 0.3s ease;
  display: block;
  margin: 1.25rem auto 0;

  &:hover {
    background: #449b8a;
  }
}

/* =========================================================
   3️⃣ 내부 정렬 및 반응형 유지
========================================================= */

@media (max-width: 64rem) { /* 1024px */
  .reserve-container {
    grid-template-columns: 1fr;
    gap: 1.25rem;
  }

  .form_card,
  .summary_card,
  .payment_card {
    width: 90%;
    margin-inline: auto;
  }

  .summary_card {
    width: 100%;
  }
}
</style>
