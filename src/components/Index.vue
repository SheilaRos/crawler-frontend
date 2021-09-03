<template>
 <div class="container h-100 align-content-center">
        <h1>Crawler</h1>
        <div class="h-100 container">
                <form id="app-crawler" class="align-content-center" v-on:submit.prevent="runCrawler">
                    <div class="row">
                            <div class="form-group col-sm-9">
                                <label for="form-crawl-url">Url</label>
                                <input class="form-control" type="text" id="url" v-model="url" required placeholder="paste your url...">
                            </div>
                            <div class="form-group col-sm-2">
                                <label for="form-crawl-depth">Depth</label>
                                <input class="form-control" type="number" id="depths" v-model="depths" required placeholder="crawl depth?">
                            </div>

                            <div class="form-group col-sm-1">
                                <input type="submit" class="form-control btn-info  btn-align" value="Search!">
                            </div>
                    </div>
                </form>
        </div>
        <div id="result">
            {{listUrls}}
        </div>
    </div>
</template>

<style scoped>
  .btn-align{
      margin-top: 22px;
  }
  #crawl_play{
    color: white;
  }

</style>
<script>
import axios from 'axios';

export default{
    name: 'Crawler',
    data: function(){
        return{
            url: "",
            depths: ""
        }
    },
    methods:{
        async runCrawler(){
            document.getElementById('result').innerHTML = "";
            let json = {
                "url": this.url,
                "depths": this.depths
            };

           await axios.post('http://localhost:3002/run-crawler', json)
            .then(
                data => {
                   document.getElementById('result').innerHTML = '<hr><h1>Result Visit Urls</h1><p>'+data.data.split(',').join('<br>')+'</p>';
                }
            )
        }
    }
}
</script>

