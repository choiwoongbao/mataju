<template>
  <div class="info-inner">
  <section class="dont-list">
      <div class="dont-head">
        <h3 class="dont-title">보관 불가 품목</h3>
        <p class="dont-sub">이런 품목은 보관이 어렵습니다</p>
      </div>

      <ul class="subject-wrap">
        <!-- cash -->
        <li class="ban-list">
          <span class="ban-icon"> </span>
          <p class="ban-text">공공기관에서는 보관함에 <strong>현금</strong>을 넣어두라고 요구하지 않습니다.</p>
        </li>

        <!-- 2. 음식물 -->
        <li class="ban-list">
          <span class="ban-icon">
            <svg viewBox="0 0 448 512" aria-hidden="true">
              <path
                d="M352 111.1c22.09 0 40-17.88 40-39.97S352 0 352 0s-40 49.91-40 72S329.9 111.1 352 111.1zM224 111.1c22.09 0 40-17.88 40-39.97S224 0 224 0S184 49.91 184 72S201.9 111.1 224 111.1zM383.1 223.1L384 160c0-8.836-7.164-16-16-16h-32C327.2 144 320 151.2 320 160v64h-64V160c0-8.836-7.164-16-16-16h-32C199.2 144 192 151.2 192 160v64H128V160c0-8.836-7.164-16-16-16h-32C71.16 144 64 151.2 64 160v63.97c-35.35 0-64 28.65-64 63.1v68.7c9.814 6.102 21.39 11.33 32 11.33c20.64 0 45.05-19.73 52.7-27.33c6.25-6.219 16.34-6.219 22.59 0C114.1 348.3 139.4 367.1 160 367.1s45.05-19.73 52.7-27.33c6.25-6.219 16.34-6.219 22.59 0C242.1 348.3 267.4 367.1 288 367.1s45.05-19.73 52.7-27.33c6.25-6.219 16.34-6.219 22.59 0C370.1 348.3 395.4 367.1 416 367.1c10.61 0 22.19-5.227 32-11.33V287.1C448 252.6 419.3 223.1 383.1 223.1zM352 373.3c-13.75 10.95-38.03 26.66-64 26.66s-50.25-15.7-64-26.66c-13.75 10.95-38.03 26.66-64 26.66s-50.25-15.7-64-26.66c-13.75 10.95-38.03 26.66-64 26.66c-11.27 0-22.09-3.121-32-7.377v87.38C0 497.7 14.33 512 32 512h384c17.67 0 32-14.33 32-32v-87.38c-9.91 4.256-20.73 7.377-32 7.377C390 399.1 365.8 384.3 352 373.3zM96 111.1c22.09 0 40-17.88 40-39.97S96 0 96 0S56 49.91 56 72S73.91 111.1 96 111.1z" />
            </svg>
          </span>
          <p class="ban-text">
            <strong>음식물</strong> 보관 시 부패나 악취로 인해 사전에 경고 없이 폐기처분될 수 있습니다.
          </p>
        </li>

        <!-- 3. 귀중품 -->
        <li class="ban-list">
          <span class="ban-icon">
            <!-- 다이아 -->
            <svg id="icons" viewBox="0 0 512 512" aria-hidden="true">
              <path
                d="M35.42,188.21,243.17,457.67a16.17,16.17,0,0,0,25.66,0L476.58,188.21a16.52,16.52,0,0,0,.95-18.75L407.06,55.71A16.22,16.22,0,0,0,393.27,48H118.73a16.22,16.22,0,0,0-13.79,7.71L34.47,169.46A16.52,16.52,0,0,0,35.42,188.21Z"
                fill="none"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32" />
              <line
                fill="none"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32"
                x1="48"
                x2="464"
                y1="176"
                y2="176" />
              <polyline
                fill="none"
                points="400 64 352 176 256 48"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32" />
              <polyline
                fill="none"
                points="112 64 160 176 256 48"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32" />
              <line
                fill="none"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32"
                x1="256"
                x2="160"
                y1="448"
                y2="176" />
              <line
                fill="none"
                stroke="#000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="32"
                x1="256"
                x2="352"
                y1="448"
                y2="176" />
            </svg>
          </span>
          <p class="ban-text">도난 우려가 있는 <strong>귀중품</strong>은 보관이 어렵습니다.</p>
        </li>

        <!-- 4. 위험물 -->
        <li class="ban-list">
          <span class="ban-icon">
            <!-- 경고 삼각형 -->
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <path d="M12 3l10 18H2L12 3Z" />
              <circle cx="12" cy="17" r="1.5" />
              <path d="M12 9v5" />
            </svg>

       
          </span>
          <p class="ban-text">
            폭발 위험이 있는 <strong>위험물</strong><small> (ex. 라이터, 부탄가스 등)</small> 보관이 어렵습니다.
          </p>
        </li>

        <!-- 5. 생명체 -->
        <li class="ban-list">
          <span class="ban-icon">
            <!-- 잎사귀 -->
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <path d="M21 3s-6 .2-10 4c-4 3.8-4 10-4 10s6 .2 10-3.6C21 9.8 21 3 21 3Z" />
              <path d="M3 21c6-6 9-9 18-18" />
            </svg>
          </span>
          <p class="ban-text">동물과 식물 등 호흡을 하는 모든 <strong>생명체</strong>는 보관이 불가합니다.</p>
        </li>
      </ul>

      <div class="ban-note">
        <p class="ban-note1">※ 보관 불가 품목을 보관해서 일어난 일에 대해서 회사는 책임을 지지 않습니다.</p>
        <p class="ban-note1">※ 안내된 물건 외에 문의가 필요해 보이는 품목은 고객센터에 문의해 주세요.</p>
      </div>
    </section>
  </div>
</template>

<script setup></script>
<style scoped>
.info-inner {
  box-sizing: border-box;
  max-width: 1100px;
  width: 100%;
  margin: 0 auto;
}
/* dont */
.dont-list {
  max-width: 1200px;
  margin: 110px auto;
}

.dont-head {
  margin-bottom: 40px;
}

.dont-title {
  font-size: 32px;
  color: #000;
  font-weight: 800;
}
.dont-sub {
  font-size: 18px;
  color: #555353;
}

.subject-wrap {
  list-style: none;
  margin: 0px 0 12px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.ban-list {
  display: flex;
  align-items: center;
  background-color: #fff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
  gap: 20px;
  border-radius: 20px;
  padding: 15px 18px;
}

.ban-icon {
  flex: 0 0 auto;
  width: 50px;
  height: 50px;
  border-radius: 9999px;
  display: grid;
  place-items: center;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}
.ban-icon svg {
  width: 30px;
  height: 30px;
  fill: #028587;
}

.ban-text {
  font-size: 18px;
  font-weight: 500;
  line-height: 1.6;
}
.ban-text strong {
  font-weight: 800;
  color: #000;
}
.ban-text small {
  color: #b8b3b3;
  font-size: 15px;
}
.ban-note {
  margin-top: 20px;
  text-align: center;
}
.ban-note1 {
  font-size: 14px;
  color: #555353;
  font-weight: 400;
}
</style>



