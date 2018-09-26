<template>
    <div>
        <vHeader></vHeader>
        <div class="article_list">
            <ul>
                <li v-for="i in list" :key="i.id">
                    <time v-text="$utils.goodTime(i.create_at)"></time>
                    <router-link :to="'/content/' + i.id">
                        {{ i.title }}
                    </router-link>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import vHeader from '../components/header.vue'
import vFooter from '../components/footer.vue'
export default {
    components: { vHeader, vFooter },
    data() {
        return {
            list: []
        }
    },
    created() {
        this.getData()
    },
    methods: {
        getData() {
            this.$api.get('topics', null, r => {
                this.list = r.data
            })
        }
    }
}
</script>
