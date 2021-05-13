<template>
  <div class="hello">
    <h1 @click="download">{{ msg }}</h1>
  </div>
</template>

<script>
/* eslint-disable */ 
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '下载文件'
    }
  },
  methods: {
      download() {
        var xhr = new XMLHttpRequest();
        var formData = new FormData();
        //url填写后台的接口地址
        xhr.open('get','https://www.wkjyqh.com/upload/20151217/20151217235845697.xls');  
        xhr.responseType = 'blob';
        xhr.onload = function (e) {
            if (this.status == 200) {
                var blob = this.response;
                var filename = "导出文件.xls";
                console.log(this.response)
                if (window.navigator.msSaveOrOpenBlob) {
                    navigator.msSaveBlob(blob, filename);
                } else {
                var a = document.createElement('a');
                var url = URL.createObjectURL(blob);
                a.href = url;
                a.download = filename;
                document.body.appendChild(a);
                a.click();
                window.URL.revokeObjectURL(url);
                }
            }
        }
        xhr.send(formData);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
