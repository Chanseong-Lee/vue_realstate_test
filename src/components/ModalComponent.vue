<template>
  <div class="black-bg" v-if="is_modal_opend"> <!-- v-if안에 값이 참일경우에만 해당 코드를 보여줌 -->
    <div class="white-bg">
      <img class="modal_img" :src="rooms[clickedRoomIdx].image">
      <h4>{{rooms[clickedRoomIdx].title}}</h4>
      <p>{{rooms[clickedRoomIdx].content}}</p>
      <p>{{rooms[clickedRoomIdx].price}}원</p>
      <DiscountComponent/>
      <button @click="close_modal">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
    name: "ModalComponent",
}
</script>
<style>

</style>