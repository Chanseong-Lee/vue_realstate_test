<template>
    <div>
        <img :src="room.image" class="room-img">
        <h4 @click="$emit('openModal', room.id)"> {{ room.title }}</h4> <!-- $emit()을 사용하면 부모에게 메시지를 줄 수 있음-->
        <p>{{ room.price }}원</p>
    </div>
</template>
<script>
export default {
    name:"CardComponent",
    props: { //props로 받아온 데이터는 수정금지(Read-only) -> Custom Event로 부모에게 메시지를 날려 부모의 데이터를 바꿀수 있음
        room : Object,
    }
}
</script>
<style>
    
</style>