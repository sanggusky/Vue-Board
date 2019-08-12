<template>
    <div>
      <!--양방향 통신이 가능하도록 v-model 사용-->
      <input v-model="writer" placeholder="글쓴이"/>
      <input v-model="title" placeholder="제목"/>
      <textarea v-model="content" placeholder="내용"/>
      <button @click="index !== undefined ? update() : write()">{{index !== undefined ? '수정' : '작성'}}</button>
    </div>
</template>
<script>
import data from '@/data'

export default {
    name: 'Create', 
    data() {
        const index = this.$route.params.contentId;
      return {
        data: data,
        index: index,
        writer: index !== undefined ? data[index].writer :  "",
        //만약에 가져온 index가 undefinded가 아니면 객체의 writer를 가져오고 없으면 빈 상태로 둔다.
        title: index !== undefined ? data[index].title :  "",
        content: index !== undefined ? data[index].content :  "", 
      }  
    },
    //새글을 작성하려면 test Data 배열에 형식에 객체를 추가
    methods: {
        write() {
          this.data.push({
            //가져온 데이터에 객체 push
              writer: this.writer,
              title: this.title,
              content: this.content,
          })
          //다시 경로로 돌아간다.
          this.$router.push({
              path: '/'
          })
        },
        update() {
            data[this.index].writer = this.writer
            data[this.index].title = this.title
            data[this.index].content = this.content
            this.$router.push({
                path: '/'
            }) 
        }
    }
}
</script>