<template>
    <div id="app">
        <!--   <router-view/> -->
        <Tree class='tree' :dataTree='msg'></Tree>
        <!-- right -->
        <Tab class='tab' v-model='tabActive' :tabItems='tabItems' @closeTabItem='closeTabItem'>
            <TabItem v-for='item in tabItems' :itemName='item'>
                <!-- <Taba :tabItem='item'></Taba> -->
                <component v-bind:is="item.comName" :tabItem='item'></component>
            </TabItem>
        </Tab>
    </div>
</template>
<script type="text/ecmascript-6">
import Tree from './views/Tree.vue'
import Tab from './views/Tab.vue'
import TabItem from './views/tab-item.vue'

import Taba from './views/Taba.vue'
import Tabb from './views/Tabb.vue'
import Tabc from './views/Tabc.vue'

import { commonMsg } from './commonMsg';

export default {
    components: {
        'Tree': Tree,
        Tab,
        TabItem,
        Tabb,
        Taba,
        Tabc
    },
    data: () => {
        return {
            tabActive: '',
            // tabItems: [{ showName: '中国', 'tabActive': 'tab_1' },{ showName: '美国', 'tabActive': 'tab_2' },{ showName: '澳大利亚', 'tabActive': 'tab_3' }],
            tabItems: [],

            msg: [{
                    name: '一级',
                    par: 0,
                    state: 'open',
                    children: [{
                            name: '一级-1',
                            par: 1,
                            state: 'open',
                            children: [
                                { name: '一级-1-1', par: 1, state: 'close', children: [], showName: '中国', 'tabActive': 'tab_1', comName: 'taba' },
                                { name: '一级-1-2', par: 1, state: 'close', children: [], showName: '美国', 'tabActive': 'tab_2', comName: 'tabb' }
                            ]
                        },
                        {
                            name: '一级-2',
                            par: 1,
                            state: 'close',
                            children: [
                                { name: '一级-2-1', par: 1, state: 'close', children: [], showName: '澳大利亚', 'tabActive': 'tab_3', comName: 'tabc' },
                                { name: '一级-2-2', par: 1, state: 'close', children: [], showName: '德国', 'tabActive': 'tab_4', comName: 'taba' }

                            ]
                        }
                    ]
                },
                {
                    name: '二级',
                    par: 0,
                    state: 'close',
                    children: [
                        { name: '二级-1', par: 1, state: 'close', children: [], showName: '法国', 'tabActive': 'tab_5', comName: 'taba' },
                        { name: '二级-2', par: 1, state: 'close', children: [], showName: '加拿大', 'tabActive': 'tab_6', comName: 'tabc' }
                    ]
                }
            ]
        }
    },
    methods: {
        // 关闭 一个标签
        closeTabItem(item){
            let index = this.tabItems.indexOf(item);
            if(index>=0){
                this.tabItems.splice(index,1);
                if(item.tabActive === this.tabActive){
                    this.tabActive = '';
                    // let index = ((index-1 >=0) ? index-1 :this.tabItems.length);
                    if(index-1>=0){
                        index = index-1;
                    }else{
                        index = this.tabItems.length-1;
                    }
                    // this.tabActive = this.tabItems.length>0 ? this.tabItems[index].tabActive : '';
                    if(this.tabItems.length>0){
                        this.$nextTick(()=>{
                            this.tabActive = this.tabItems[index].tabActive
                        })
                    }
                }
            }
        }
    },
    created() {
        commonMsg.registerEvents('eventTabChange', '', (dataBack) => {
            // 如果原来没有，加入，如果原来有，不用加入
            if (!this.tabItems.find(item => item.tabActive === dataBack.tabActive)) { // 注意 .find 的用法
                this.tabItems.push(dataBack);
                this.tabActive = dataBack.tabActive;
            }
        })
    }
};
</script>
<style lang="scss">
.clearfix:after {
    content: "";
    display: block;
    clear: both;
}

html,
body,
#app {
    height: 100%;
    margin: 0;
}

// public class start =========================================================
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale; // text-align: center;
    color: #2c3e50;
    .fl {
        float: left;
    }
    .fr {
        float: right;
    }
}

// public class start =========================================================
#app {
    box-sizing: border-box;
    position: relative;
    .tree {
        // width: 200px;
        // height: 100%;
        position: absolute;
        width: 300px;
    }
    .tab {
        width: 100%;
        padding-left: 300px;
    }
}
</style>