<template>
    <div>
        <list ref="list" :show-scrollbar="false" :showRefresh="true" @refresh="onrefresh">
            <cell v-for="(num, index) in arr" :key="index" :index="index">
                <wxc-cell :title="`这是第${num}条数据`"
                    :has-arrow="false"
                    @wxcCellClicked="wxcCellClicked"
                    :has-top-border="true"></wxc-cell>
            </cell>
        </list>
        <div class="touch-bar" :style="{'height': touchBarHeight}">
        </div>
    </div>
</template>
<script>
import { WxcCell } from 'weex-ui'
export default {
    components: { WxcCell },
    data () {
        return {
            arr: [],
            touchBarHeight: weex.config.eros.touchBarHeight ? weex.config.eros.touchBarHeight : 0
        }
    },
    created () {
        for (let i = 0; i < 20; i++) {
            this.arr.push(i + 1)
        }
    },
    methods: {
        onrefresh () {
            setTimeout(() => {
                this.$refs['list'].refreshEnd()
                this.$notice.toast({
                    message: 'refreshEnd'
                });
            }, 1000)
        }
    }
}

</script>
<style lang="sass" scoped>
@import 'src/js/css/base';
.container {
    width: 700px;
    margin: 25px;
}
</style>
