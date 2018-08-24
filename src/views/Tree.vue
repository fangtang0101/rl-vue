<template>
    <div id='main'>
        <ul v-for='item in dataTree' @click.stop='changeState(item)' v-bind:style="{  paddingLeft: (item.par*10)+20 +  'px' }">
            {{item.name}}
            <li v-for='item2 in item.children' v-if="item.state == 'open'" @click.stop='changeState(item2)'>
                {{item2.name}}
                <tree v-if="item2.state == 'open'" :dataTree='item2.children'></tree>
            </li>
        </ul>
    </div>
</template>
<script type="text/ecmascript-6">
import {commonMsg} from '../commonMsg';
export default {
    name: 'tree',
    props: {
        dataTree: {
            type: Array,
            'default': true
        }
    },
    data() {
        return {}
    },
    methods: {
        changeState(item) {
            item.state = item.state === 'open' ? 'close' : 'open';
            if(item.tabActive){
                 commonMsg.sendEvents('eventTabChange',item);
            }
        },
    }
};
</script>
<style lang="scss" rel="stylesheet/scss">
#main {
    box-sizing: border-box;
    ul {
        background-color: #efefef;
        li {
            background-color: #999;
        }
    }
    ul,
    li {
        max-width: 300px;
        padding: 0;
        margin: 0;
        list-style: none;

        text-align: left;
        cursor: pointer;
    }
}
</style>