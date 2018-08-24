<template>
    <div v-if='tabItem'>
    	<div>组件名字: Tabb.vue</div>
    	<div> 级别:{{tabItem.name}}</div>
    	<div>显示名字:{{tabItem.showName}}</div>
    </div>
</template>
<script type="text/ecmascript-6">
export default {
    name: 'tabb',
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
    created() {
        console.log('created ... tab-b');
    },
    mounted() {
        console.log('mounted ... tab-b');
    },
};
</script>
<style lang="scss"></style>