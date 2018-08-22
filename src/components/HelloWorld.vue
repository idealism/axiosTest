<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input v-model="userId" />
    <h2>{{ userName }}</h2>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',

  data:function () {
     return {
       userId:'',
      userName:''
     }
  },
  props: {
    msg: String
  },
  watch:{
    userId:function(newValue){
      let _this = this;
      this.axios.get('user.json').then(function(res){
        _this.userName = '';
        res.data.forEach(element => {
          if(element.userId == newValue){
            _this.userName = element.userName;
          }
        });
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
