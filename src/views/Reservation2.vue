<template>
  <section class="reserve-page">
    <div class="inner">
      <Stepper :current-step="2" />

      <div class="wrap_reserv">
        <!-- 위쪽 2개 카드 (Grid 정렬) -->
        <div class="reserve-container">
          <!-- 사물함 예약 카드 -->
          <div class="form_card line">
            <div class="card_header">
              <h2>정보</h2>
            </div>
            <div class="card_content">
              <table>
                <tbody>
                  <tr>
                    <td>성함</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>휴대폰</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>사물함사이즈</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>대여장소</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>예약날짜</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>픽업장소</td>
                    <td>사물함 대여</td>
                  </tr>
                  <tr>
                    <td>배송지정일1</td>
                    <td>입력 필요</td>
                  </tr>
                  <tr>
                    <td>주소</td>
                    <td>입력 필요</td>
                  </tr>
                  <tr>
                    <td>상세주소</td>
                    <td>입력 필요</td>
                  </tr>
                  <tr>
                    <td>배송일2</td>
                    <td>입력 필요</td>
                  </tr>
                  <tr class="total">
                    <td>총 결제금액</td>
                    <td><strong>29,000원</strong></td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- 선택 상품 요약 카드 -->
          <div class="summary_card line">
            <h2 class="card_title">선택 상품 요약</h2>
            <ul>
              <li v-for="tab in selectedTabs" :key="tab">{{ tab }} — {{ formatKrw(prices[tab]) }}</li>
            </ul>

            <div class="divider"></div>

            <div class="benefits">
              <h4>마일리지 / 쿠폰 사용</h4>
              <div class="benefit-row">
                <label class="inline">
                  <input type="checkbox" v-model="useCoupon" />
                  Welcome 쿠폰 - 3,000원
                </label>
                <span class="muted" v-if="useCoupon"> - {{ formatKrw(3000) }} </span>
              </div>

              <div class="benefit-row">
                <label class="inline">
                  <input type="checkbox" v-model="usePoints" />
                  포인트 - 2,500P
                </label>
                <span class="muted" v-if="usePoints"> - {{ formatKrw(2500) }} </span>
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
            <div class="card_header">
              <h3>결제방법 선택</h3>
            </div>
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

const totalPrice = computed(() => selectedTabs.value.reduce((sum, tab) => sum + prices[tab], 0));

const discountAmount = computed(() => {
  let discount = 0;
  if (useCoupon.value) discount += 3000;
  if (usePoints.value) discount += 2500;
  return Math.min(discount, totalPrice.value);
});

const finalTotal = computed(() => Math.max(totalPrice.value - discountAmount.value, 0));

const paymentMethods = [
  { id: "card", label: "신용카드", icon: "💳" },
  { id: "kakao", label: "카카오페이", icon: "💬 pay" },
  { id: "naver", label: "네이버페이", icon: "N pay" },
  { id: "bank", label: "무통장입금", icon: "🏦" },
];

const formatKrw = (v) =>
  new Intl.NumberFormat("ko-KR", {
    style: "currency",
    currency: "KRW",
  }).format(v);

const paymentLabel = computed(() => {
  const m = paymentMethods.find((p) => p.id === selectedPayment.value);
  return m ? m.label : "-";
});

const saveAndPay = () =>
  alert(`✅ 결제가 완료되었습니다!\n결제수단: ${paymentLabel.value}\n결제금액: ${formatKrw(finalTotal.value)}`);
</script>

<style lang="scss" scoped>
/* =========================================================
   💳 Reservation3 — 고정형 레이아웃 (max-width: 1320px)
========================================================= */
.reserve-page {
  background: #f5f7f7;
  min-height: 60rem;
  width: 100%;
  padding: 5rem 0;
  overflow-x: hidden;
}

.inner {
  width: 100%;
  max-width: 1120px; /* ✅ 고정 폭 제한 */
  margin: 0 auto;
  // padding: 0 1.5rem; /* ✅ 여백 살짝 (양쪽 24px) — 선택사항 */
  box-sizing: border-box;
}
.reserve-container {
  width: 100%;
  max-width: 1320px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 2.5rem;
  align-items: start;
}

.paysection {
  width: 100%;
  max-width: 1320px;
  margin: 3.75rem auto 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* 카드 공통 */
.form_card,
.summary_card,
.payment_card {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  padding: 30px 40px;
  position: relative;
  border: 1px solid transparent;
  // transition: all 0.3s ease;

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 8px;
    background: #53b4a1;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }
}

/* ✅ 첫 번째 카드 표 정렬 수정 */
.form_card table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.875rem;
  color: #333;

  td {
    padding: 0.4rem 0.6rem;
    text-align: left;
    vertical-align: middle;
    line-height: 1.4;
  }

  td:first-child {
    width: 40%;
    color: #666;
    font-weight: 500;
  }

  td:last-child {
    width: 60%;
    color: #222;
  }

  tr.total {
    border-top: 1px solid #ddd;
    td:last-child {
      color: #53b4a1;
      font-weight: 700;
    }
  }
}

/* Summary 카드 */
.summary_card {
  // width: 400px;

  .card_title {
    font-size: 18px;
    font-weight: 600;
    color: #222;
    margin-bottom: 20px;
  }

  ul {
    font-size: 14px;
    color: #444;
    margin-bottom: 24px;
  }
}

/* 결제 카드 */
.payment_card {
  width: 100%;

  .pay-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 20px;
  }

  .pay-card {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    padding: 16px 0;
    border: 1px solid #ddd;
    border-radius: 8px;
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
      font-size: 18px;
    }
  }
}

/* 결제 버튼 */
.submit_btn {
  width: 70%;
  padding: 14px 0;
  font-weight: 600;
  font-size: 15px;
  color: #fff;
  background: #53b4a1;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  // transition: 0.3s ease;
  display: block;
  margin: 20px auto 0;

  &:hover {
    background: #449b8a;
  }
}

/* 반응형 */
@media (max-width: 1024px) {
  .reserve-container {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .form_card,
  .summary_card,
  .payment_card {
    width: 90%;
    margin-inline: auto;
  }

  .paysection {
    margin-top: 2rem;
  }
}
/* =========================================================
   4️⃣ 내부 구조 & 요약 카드 세부 스타일 보완
========================================================= */

/* wrap_reserv : 전체 상·하단 구역 간격 */
.wrap_reserv {
  display: flex;
  flex-direction: column;
  gap: 3rem; /* 위아래 카드 간 간격 */
}

/* 카드 내부 기본 구조 */
.card_header {
  margin-bottom: 1rem;

  h3 {
    font-size: 1rem;
    font-weight: 600;
    color: #222;
    margin: 0;
  }
}

.card_content {
  margin-top: 0.5rem;
}

/* Summary 카드 내부 세부요소 */
.divider {
  height: 1px;
  background: #eee;
  margin: 1.25rem 0;
}

.benefit-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;

  label {
    font-size: 0.875rem;
    color: #333;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
}

.muted {
  color: #d72638;
  font-size: 0.8125rem;
  font-weight: 500;
}

.total-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.9375rem;
  font-weight: 600;
  color: #222;
  margin-top: 1rem;

  strong {
    color: #53b4a1;
  }
}
</style>
