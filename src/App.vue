<template>
  <div class="menu">
    <!-- <a v-for="변수명 in 반복할 숫자" :key="변수명">Home</a> -->
    <!-- <a v-for="변수명 in 배열" :key="변수명">{{ 변수명 }}</a> -->
    <!-- <a v-for="(변수명, ksy변수명) in 배열" :key="key변수명">{{ 변수명 }}</a> -->
    <!-- key속성은 유니크한 자료를 넣는다-->
    <!-- 반복문은 변수 작명 2개까지 가능. 왼쪽변수는 array데이터, 오른쪽변수는 1씩증가하는 정수 -->
    <!-- <a v-for="(item, i) in menus" :key="i">{{ i }}</a> -->
    <a v-for="item in menus" :key="item">{{ item }}</a>
  </div>
  <!-- <div v-for="a, i in 3" :key="i"> -->
    <!-- <h4 class="red" :style="styleBinding">{{ products[i] }}</h4> 속성앞에 :을 붙이면 프로퍼티도 바인딩 가능 -->
    <!-- <p>{{ prices[i] }} 만원 {{ a }}</p> {{data binding}} -->
  <!-- </div> -->
  <div>
    <h4>{{ products[0] }}</h4>
    <p>{{ prices[0] }}만원</p>
    <button @click="increase(0)">허위매물신고</button> 
    <span>신고수 : {{ report_num[0] }}</span> <!-- onClick속성은 v-on:click이고 축약하면 @click -->
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ prices[1] }}만원</p>
    <button @click="increase(1)">허위매물신고</button> 
    <span>신고수 : {{ report_num[1] }}</span>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ prices[2] }}만원</p>
    <button @click="increase(2)">허위매물신고</button> 
    <span>신고수 : {{ report_num[2] }}</span>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      //{{데이터 바인딩}}을 위한 데이터 보관 : 실시간 자동 렌더링을 쓰려면 이런식으로 관리
      // 자주 변경될 데이터를 주로 보관
      styleBinding: 'color : blue',
      menus: ["Home", "Shop", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      prices: [60, 70, 80],
      report_num: [0, 0, 0],
    }
  },
  methods: {
    increase(i) {
      //report_num은 현재 블록에 정의가 안되있기때문에 data()의 report_num을 가져오기위해 this키워드를 사용. this는 상위 오브젝트를 의미
      this.report_num[i]++;
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
