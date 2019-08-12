<template>
    <div>
       <table>
        <tr>
            <td>글쓴이</td>
            <td>제목</td>
            <td>내용</td>
        </tr>
        <tr :key="index" v-for="(value, index) in data" @click="detail(index)">
            <!--배열을 기반으로 리스트를 렌더링 할 수 있다-->  
            <!--클릭한 글에 index를 보내준다-->         
            <td>{{value.writer}}</td>
            <td>{{value.title}}</td>
            <td>{{value.content}}</td>
        </tr>
       </table>
       <button @click="write">글쓰기</button>
    </div>
</template>
<script>
import data from '@/data'

export default {
    name: 'Read',
    data() {
        return {
            data: data
        }
    },
    methods: {
        write() {
            this.$router.push({
                path: 'create'
             })
        },
        detail(index) {
            this.$router.push({
                name: 'Detail',
                params: {
                    contentId: index
                }
            })
        }
    }    
}
</script>