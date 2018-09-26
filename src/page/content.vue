<template>
    <div>
        <vHeader></vHeader>
        <h2 v-text="data.title"></h2>
        <p>作者: {{ data.author.loginname }}  --  {{ $utils.goodTime(data.create_at) }}</p>
        <hr>
        <article v-html="data.content"></article>
        <h3>网友回复:</h3>
        <ul>
            <il v-for="i in data.replies" :key="i.id">
                <p>评论者: {{ i.author.loginname }}</p>
                <article v-html="i.content"></article>
            </il>
        </ul>
        <vFooter></vFooter>
    </div>
</template>

<script>
import vHeader from '../components/header.vue'
import vFooter from '../components/footer.vue'
export default {
    components: { vHeader, vFooter },
    data() {
        return {
            id: this.$route.params.id,
            data: {}
        }
    },
    created() {
        this.getData()
    },
    methods: {
        getData() {
            this.$api.get('topic/' + this.id, null, r => {
                this.data = r.data
            })
        }
    }
}
</script>
