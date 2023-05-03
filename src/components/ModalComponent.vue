<template>
  <div class="black-bg" v-if="is_modal_opened"> <!-- v-if안에 값이 참일경우에만 해당 코드를 보여줌 -->
    <div class="white-bg">
      <img class="modal_img" :src="rooms[clickedRoomIdx].image">
      <h4>{{rooms[clickedRoomIdx].title}}</h4>
      <p>{{rooms[clickedRoomIdx].content}}</p>
      <!-- @input 입력할때마다 이벤트 실행, @change는 입력하고 다른곳 클릭할때 -->
      <!-- 이벤트리스너를 불러올때 $event로 불러옴, target은 현재 이벤트가 발생한곳 -->
      <!-- <input @input="month = $event.target.value">  -->
      <input v-model="month"> <!-- 위 주석의 축약버전 -->

      <p> {{ month }}개월 선택함 : {{rooms[clickedRoomIdx].price * month}}원</p>
      <button @click="send">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
    name: "ModalComponent",
    data(){
      return {
        month: 1, //초기값의 자료형이 중요함 하지만 input은 저장은 넘버여도 문자로 저장됨
      }
    },
    watch : { //데이터를 감시하는 함수들의 집합
      month(newParam, oldParam){  //watch함수명을 data()에 정의된 변수명과 일치시킴, month의 값이 변경될 때 마다 실행됨
        // 사용자가 month를 숫자가 아닌타입의 자료를 넣으면 alert을 띄운다.
        
        const regex = /^[0-9]+$/g; //숫자 정규 표현식
        if(newParam.length > 0){
          if(!regex.test(newParam)){
            alert("숫자만 입력하실 수 있습니다.");
            this.month = oldParam;
          }
          // else if(newParam == 2){
          //   alert("2개월은 안팔아요")
          //   this.month = oldParam;
          // }
        }
        // if(isNaN(newParam)){ //숫자면 false, 숫자가 아니면 true
        //   alert("숫자만 입력하실 수 있습니다.")
        //   this.month = oldParam;
        // }
      }
    },
    props : { //App.vue에서 v-bind로 넘겨준 데이터를 props에서 등록
      rooms : Array,  // v-bind의 변수명 : 자료형
      is_modal_opened : Boolean,
      clickedRoomIdx: Number, ////props로 받아온 데이터는 수정금지(Read-only) -> Custom Event로 부모의 데이터를 바꿀수 있음
      close_modal: Function
    },
    methods : {
      send(){
        this.$emit("closeModal")
      },
    },
    beforeUpdate(){
      if(this.month == 2){
        alert("2개월은 안팔아요")
        this.month = '';
      }
    },
}
</script>
<style>

</style>