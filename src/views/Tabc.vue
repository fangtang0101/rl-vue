<template>
    <div v-if='tabItem'>
    	<div>组件名字: Tabc.vue</div>
    	<div> 级别:{{tabItem.name}}</div>
    	<div>显示名字:{{tabItem.showName}}</div>
    </div>
</template>
<script type="text/ecmascript-6">
export default {
    name: 'tabc',
    components: {},
    props: {
    	tabItem:{
    		type:Object,
    		'default':null
    	}
    },
    data: () => {
        return {}
    },
    methods: {
    },
    created() {},
    mounted() {},
};
</script>
<style lang="scss"></style>