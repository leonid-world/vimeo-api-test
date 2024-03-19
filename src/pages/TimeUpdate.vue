<template>
    <div>
        <div style="width:300px; height: 400px;">
            <iframe
                src="https://player.vimeo.com/video/882455373?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479"
                frameborder="0"
                allow="autoplay; fullscreen; picture-in-picture; clipboard-write"
                style="width:100%;height:100%;"
                title="IMG_0927">
            </iframe>
        </div>

        <q-btn @click="getPlayed"> getPlayed </q-btn>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

let player = null;


onMounted(() => {
    const iframe = document.querySelector('iframe');
    player = new Vimeo.Player(iframe);

    //플레이 시, 시간 지날때마다 이벤트 호출
    player.on('timeupdate',function(data) {
        console.log('time update seconds : ', data.seconds);
    })
    

    player.pause().then(function() {
        console.log('paused')
    })
    
})

//플레이한 시간만큼 데이터 가져오기
const getPlayed = () => {

    player.getPlayed().then(function(played) {
        console.log('played : ', played);
    })
}
</script>

<style lang="scss" scoped></style>
