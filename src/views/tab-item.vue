<template>
    <div>
        <div v-if='itemName' v-show='isShow'><slot></slot></div>
    </div>
</template>
<script type="text/ecmascript-6">
export default {
    name: 'tab-item',
    components: {},
    computed: {
        isShow() {
            let show = false;
            if (this.$parent && this.$parent.tabActive && this.itemName && this.itemName.tabActive) {
                if (this.$parent.tabActive === this.itemName.tabActive) {
                    show = true;
                }
            }
            return show;
        }
    },
    props: {
        itemName: {
            type: Object,
            'default': null
        }
    },
    data: () => {
        return {}
    },
    methods: {},
};
</script>
<style lang="scss">
</style>