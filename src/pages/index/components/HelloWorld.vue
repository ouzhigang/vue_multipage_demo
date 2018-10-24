<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <h2>Essential Links</h2>
        <ul>
            <li>
                <a href="https://vuejs.org" target="_blank">Core Docs</a>
            </li>
            <li>
                <a href="https://forum.vuejs.org" target="_blank">Forum</a>
            </li>
            <li>
                <a href="https://chat.vuejs.org" target="_blank">Community Chat</a>
            </li>
            <li>
                <a href="https://twitter.com/vuejs" target="_blank">Twitter</a>
            </li>
            <br />
            <li>
                <a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a>
            </li>
        </ul>
        <h2>Ecosystem</h2>
        <ul>
            <li>
                <a href="http://router.vuejs.org/" target="_blank">vue-router</a>
            </li>
            <li>
                <a href="http://vuex.vuejs.org/" target="_blank">vuex</a>
            </li>
            <li>
                <a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a>
            </li>
            <li>
                <a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a>
            </li>
        </ul>
        <ul>
            <li v-for="(value, key) in cMydata">{{ value }}</li>
        </ul>
        <router-link :to="gotolist">go to list</router-link>
        <router-link :to="gotolist2">go to list2</router-link>
        <select @change="abc('ok', $event)">
            <option v-for="(value, key) in mydata" :value="key">{{ value }}</option>
        </select>
    </div>
</template>

<script>

export default {
    name: 'HelloWorld',
    data () {
        return {
            msg: 'Welcome to Your Vue.js App',
            mydata: {},
            gotolist: 'list',
            gotolist2: 'list2'
        }
    },
    mounted: function() {
        var vm = this
        var successCallback =  (response) => {
            console.log('服务器请求成功了')
            //console.log(response.data)
            vm.$set(vm, "mydata", response.data)
            console.log(vm.mydata)
        }
        var errorCallback =  (response) => {
            console.log('服务器请求出错了')
        }
        this.$http.get('/vue/testvue.php').then(successCallback, errorCallback)
    },
    methods: {
        abc: function(data, event) {
            var el = event.currentTarget
            alert(el.value)

            //this.$router.push({name: 'List', params: { id: '1' }})
            this.$router.push({path: '/list', query: { id: '2' }})
        }
    },
    computed: {
        cMydata: function () {
            var obj = {};
            for(var k in this.mydata) {
                if(k == "b") {
                    obj[k] = this.mydata[k]
                }
            }
            return obj;
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
