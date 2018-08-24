<template>
    <div id='tab'>
        <div class="tab_line">
            <span class="tab_item" v-for='item in tabItems' @click='changeTab(item)'>
                {{item.tabActive}}
                <i @click='closeTabItem(item)'></i>
            </span>
        </div>
        <div class="tab_content">
            <slot></slot>
        </div>
    </div>
</template>
<script type="text/ecmascript-6">
import tabItem from './tab-item.vue'

export default {
    name: 'tab',
    components: {
        tabItem
    },
    props: {
        tabActive: {
            type: String,
            'default': ''
        },
        tabItems: {
            type: Array,
            'default': []
        }
    },
    model: {
        prop: 'tabActive',
        event: 'tabActiveChange'
    },
    data: () => {
        return {
            // tabItems:['tab_1','tab_2','tab_3']
        }
    },
    methods: {
        changeTab(item) {
            this.$emit('tabActiveChange', item.tabActive)
        },
        closeTabItem(item){
            this.$emit('closeTabItem',item);
        }
    },
    created() {}
};
</script>
<style lang='scss'>
#tab {
    .tab_line {
        background-color: #CDBA96;
        height: 50px;
        .tab_item {
            display: inline-block;
            background-color: #efefef;
            position: relative;
            top: 20px;
            width: 50px;
            height: 30px;
            text-align: center;
            margin-right: 5px;
            line-height: 30px;
            cursor: default;
            i {
                display: inline-block;
                width: 10px;
                height: 10px;
                background-color: red;
                position: absolute;
                top:0px;
                right: 0px;
                cursor: pointer;
            }
        }
    }
}
</style>