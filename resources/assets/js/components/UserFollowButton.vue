<template>
    <a class="button" style="width: 100px" v-on:click="follow" v-html="text"
       :class="[{'is-success':!followed},{'is-light':followed}]">
    </a>
</template>

<script type="text/ecmascript-6">
    export default{
        props: ['user'],
        mounted(){
            axios.get('/api/user/followers/' + this.user).then(res => {
                this.followed = res.data.followed;
            })
        },
        data(){
            return {
                followed: false,
            }
        },
        methods: {
            follow(){
                axios.post('/api/user/followers', {'user': this.user}).then(res => {
                    this.followed = res.data.followed;
                });
            },
        },
        computed: {
            text(){
                return this.followed ? '取消关注' : `<span style="margin-right: 5px" class="icon"><i class="fa fa-plus"></i></span>关注他`;
            }
        },
    }
</script>
