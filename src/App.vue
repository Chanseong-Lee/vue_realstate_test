<!-- 
  동적인 ui만드는 법
  1. UI의 현재상태를 데이터로 저장해둠 (상태 = state / data(){} 이부분을 state라고 부름)
  2. 데이터에 따라 ui가 어떻게 보일지 작성
-->
<template>
  <!-- <div v-if="1 == 2">1 == 1</div>
  <div v-else-if="2==2">2==2</div>
  <div v-else>else</div> -->
  <!-- CSS 애니메이션 주기 : 1.시작전 class명 2.애니메이션이 끝난 후 class명 3.그리고 원할 때 2번 class명 부착 -->
  <!-- <div class="start" :class="{end : is_modal_opened}"> :class에 object형태로 바인딩 가능(조건부로 class명을 넣을 수 있음) -->
  <Transition name="fade"> <!-- transition을 위한 vue태그-->
    <ModalComponent @closeModal="is_modal_opened = false;" :rooms="rooms" :clickedRoomIdx="clickedRoomIdx" :is_modal_opened="is_modal_opened"/> <!-- v-bind: or : -->
  </Transition>
  <div class="menu">
    <!-- <a v-for="변수명 in 반복할 숫자" :key="변수명">Home</a> -->
    <!-- <a v-for="변수명 in 배열" :key="변수명">{{ 변수명 }}</a> -->
    <!-- <a v-for="(변수명, ksy변수명) in 배열" :key="key변수명">{{ 변수명 }}</a> -->
    <!-- key속성은 유니크한 자료를 넣는다-->
    <!-- 반복문은 변수 작명 2개까지 가능. 왼쪽변수는 array데이터, 오른쪽변수는 1씩증가하는 정수 -->
    <!-- <a v-for="(item, i) in menus" :key="i">{{ i }}</a> -->
    <a v-for="item in menus" :key="item">{{ item }}</a>
  </div>

  <!-- 컴포넌트 호출-->
  <DiscountComponent/>

  <!-- 상품 정렬기능 : 데이터 원본은 보존-->
  <button @click="priceSortAsc">가격순 오름차순 정렬</button>
  <button @click="priceSortDesc">가격순 내림차순 정렬</button>
  <button @click="sortBack">되돌리기</button>
  <!-- 방 리스트 -->
  <!-- 자식에서 $emit()으로 받은 메시지를 @변수명으로 받을 수 있다. $event는 자식에서 보낸 데이터를 받을 수 있다. -->
  <CardComponent @openModal="is_modal_opened = true; clickedRoomIdx = $event;" :room="rooms[i]" v-for="(room, i) in rooms" :key="room"/>
  <!-- <div v-for="(room, i) in rooms" :key="i">
        <img :src="room.image" class="room-img">
        <h4 @click="open_modal(i)"> {{ room.title }}</h4>
        <p>{{ room.price }}원</p>
  </div> -->
</template>

<script>
import data from './data/post.js' //DB없이 해당경로에 json배열로 데이터 준비하고 import
import DiscountComponent from './components/DiscountComponent.vue'; //component import
import ModalComponent from './components/ModalComponent.vue'; //component import
import CardComponent from './components/CardComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      //{{데이터 바인딩}}을 위한 데이터 보관 : 실시간 자동 렌더링을 쓰려면 이런식으로 관리
      // 자주 변경될 데이터를 주로 보관
      menus: ["Home", "Shop", "About"],
      is_modal_opened: false, //modal control
      rooms : data, //json array
      roomsOriginal : [...data], // 원본 깊은복사
      clickedRoomIdx : 0,
    }
  },
  methods: {
    increase(i) {
      //report_num은 현재 블록에 정의가 안되있기때문에 data()의 report_num을 가져오기위해 this키워드를 사용. this는 상위 오브젝트를 의미
      this.report_num[i]++;
    },
    open_modal(i){
      this.is_modal_opened = true;
      this.clickedRoomIdx = i;
    },
    close_modal (){
      this.is_modal_opened = false;
    },
    priceSortAsc(){
      this.rooms.sort(function(a, b){
        return a.price - b.price; // 음수면 왼쪽으로 보내주셈
      })
    },
    priceSortDesc(){
      this.rooms.sort(function(a, b){ //sort는 원본배열을 변형시킨다.
        return b.price - a.price; // 음수면 왼쪽으로 보내주셈
      })
    },
    sortBack(){
      this.rooms = [...this.roomsOriginal]; //원본을 깊은 복사로 대입해야한다.(그냥 대입하면 주소값을 공유하기때문에 몇번 누르면 객체가 같아지기때문)
    },
  },
  components: {
    DiscountComponent: DiscountComponent,
    ModalComponent: ModalComponent,
    CardComponent: CardComponent,
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
body{
  margin: 0px;
}
div{
  box-sizing: border-box;
}
/* start class의 모든 속성:all 이 변할때 1초가 걸림*/
/* .start {
  opacity: 0;
  transition: all 1s; 
}
.end {
  opacity: 1;
} */

/* Transition tag를 사용할 경우 : [name속성]-enter-from... */
.fade-enter-from {
  /* 시작스타일 */
  /* opacity: 0; */
  transform: translateY(-1000px);
}
.fade-enter-active {
  /* transition 동작방식 */
  transition: all 1s; 
}
.fade-enter-to {
  /* 끝스타일 */
  /* opacity: 1; */
  transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1; /* 시작스타일 */
}
.fade-leave-active {
  transition: all 1s; /* transition 동작방식 */
}
.fade-leave-to {
  opacity: 0; /* 끝스타일 */
}


.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
  /* position: fixed; */
  /* width: 100%; */
  z-index: 0;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img{
  width:100%;
  margin-top: 40px;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  z-index: 2;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.modal_img{
  width: 100%;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
div > h4:hover {
  cursor: pointer;
}
</style>
