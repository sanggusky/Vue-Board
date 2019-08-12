<template>
    <div>
      <div>{{data.writer}}</div>
      <div>{{data.title}}</div>
      <div>{{data.content}}</div>
      <button @click="updateData">수정</button>
      <button @click="deleteData">삭제</button>    
    </div>
</template>
<script>
import data from '@/data'
export default {
    name: 'Detail',
    data() {
        const index = this.$route.params.contentId
        //index는 현재 라우터의 params 속성에 있는 contentId를 가져온다
        return {
            data: data[index],
            // 데이터 배열에서 index값
            index: index,
        }
    },
    methods: {
         deleteData() {
            data.splice(this.index, 1)
            //특정 index의 요소를 삭제하는 기능 사용
            this.$router.push({
                path: '/'
            })
        },
        updateData() {
            this.$router.push({
                name: 'Create',
                params: {
                    contentId: this.index
                }
            })
        }
    }
}
</script>