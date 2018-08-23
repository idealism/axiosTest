<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input v-model="userId" />
    <h2>{{ userName }}</h2>
    <button v-on:click="promiseMethod">点击我</button>
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
  methods:{
      promiseMethod:function(){
        let promise1 = new Promise(function(resolve,reject){
            console.log('Promise1');
             resolve();
        });

        let promise2 = new Promise(function(resolve,reject){
            console.log('Promise2');
             resolve();
        });

       let promise = Promise.all([promise1,promise2]);  //race()

        promise.then(function(){
            console.log('resolved');
        });

        console.log('Hi!');
      }
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
      }).catch(function(error){
        console.log(error.message);
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
