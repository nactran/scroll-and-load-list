<template>
  <div class="container" @scroll="handleScroll">
    <div class="content">
      <div class="item" v-for="i in dataList" :key="i">{{i}}</div>
    </div>
    <div class = "list-bottom" v-if="loading">
      <div class="loading"></div>
      <p>loading</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyList',
  props: {
    msg: String
  },
  data(){
    return{
      loading: false,
      dataList: [1,2,3,4,5,6,7,8,9],
      nextData: 10
    }
  },
  methods:{
    loadData(res)
    {
      for(let i = 0; i < 10; i++){
        this.dataList.push(this.nextData);
        this.nextData++;
      }
      res();
    },
    handleScroll(e) {
      let vm = this;
      let scrollTop = e.target.scrollTop; 
      let scrollHeight = e.target.scrollHeight;
      let clientHeight = e.target.clientHeight;
      if (!vm.loading && scrollHeight - scrollTop <= clientHeight)
      {
        vm.loading = true;
        setTimeout(()=>{        
          let loadDataPromise = new Promise(vm.loadData);
          loadDataPromise.then(
            ()=>{vm.loading = false}
            );
          },
          1000
        );
      }
    }
  },
  mounted(){
    window.addEventListener('scroll',this.handleScroll,false)
  }

}
</script>

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
.container{
  overflow: auto;
  width:50%;
  min-width: 400px;
  height:300px;
  border:1px solid #d4d4d4;
}
.item {
  min-height: 60px;
  line-height:60px;
  border-bottom: 1px dashed #d4d4d4;
  width: 100%;
  text-align: center;
  /*padding: 30px 0;*/
  /*box-sizing: border-box; */
  }
  .list-bottom{
    margin-top:20px;
    padding:10px 0;
  }
  .loading{
    width: 25px;
    height: 25px;
    margin: 0 auto;
    border-radius: 50%;
    border: 4px solid #BEBEBE;
    border-left: 4px solid #498aca;
    animation: load 1s linear infinite;
    -moz-animation:load 1s linear infinite;
    -webkit-animation: load 1s linear infinite;
    -o-animation:load 1s linear infinite;
  }
  @-webkit-keyframes load
  {
    from{-webkit-transform:rotate(0deg);}
    to{-webkit-transform:rotate(360deg);}
  }
  @-moz-keyframes load
  {
    from{-moz-transform:rotate(0deg);}
    to{-moz-transform:rotate(360deg);}
  }
  @-o-keyframes load
  {
    from{-o-transform:rotate(0deg);}
    to{-o-transform:rotate(360deg);}
  }
</style>
