<template>

    <div class="author-card">
      <el-card shadow="hover">
        <el-row class="adjust-pic">
          <el-col :span="6">
            <img :src="articleAuthor.topic_user_avatar" class="author-image" />
          </el-col>
          <el-col :span="16">
            <el-row>
              <p style="padding: 5px">{{ articleAuthor.topic_user_username }}</p>
              <el-button color="#626aef" disabled size="small">Lv.{{ articleAuthor.topic_user_rank }}
              </el-button>
            </el-row>
            <el-row>
              <span style="padding: 5px">个性签名：{{ articleAuthor.topic_user_introduction }}</span>
            </el-row>
            <el-row>
              <span style="padding: 5px">发帖时间：{{ articleAuthor.create_time }}</span>
            </el-row>
          </el-col>
        </el-row>
      </el-card>

</div>


</template>

<script>
export default {
  inject:['topicId'],
  props:{articleAuthor:Object},
  data() {
    return {
      
  

    };

  },
  methods: {
    getTopicDetail() {
      let params = new URLSearchParams()
      let url = '/api/forum/getTopicDetail'
      params.append('topicId', this.topicId)
      this.$http.get(url, { params: params }).then(
        //成功
        (res) => {
          this.articleAuthor = res.data.data
        },
        //失败
        (err) => {
          console.log('error')
          console.log(err)
        }
      )
    },

  },
  mounted() {
    //this.getTopicDetail()
    console.log("author:"+this.articleAuthor)
    


  },
}
</script>

<style scoped>

.adjust-pic{
  display: flex;
  align-items: center;
}
.author-card {
  height: 150px;
  width: 100%;
}
.author-image {
  width: 50px;
  height:50px;
}

.author-card span{
  font-size: 10px;
  color: #999;
  margin: 0;
}
</style>