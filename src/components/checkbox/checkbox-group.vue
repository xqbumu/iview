<template>
    <div :class="classes">
        <slot></slot>
    </div>
</template>
<script>
    const prefixCls = 'ivu-checkbox-group';

    export default {
        name: 'CheckboxGroup',
        props: {
            value: {
                type: Array,
                default () {
                    return [];
                }
            }
        },
        data () {
            return {
                currentValue: this.value
            };
        },
        computed: {
            classes () {
                return `${prefixCls}`;
            }
        },
        mounted () {
            this.updateModel(true);
        },
        methods: {
            updateModel (update) {
                const value = this.value;

                this.$children.forEach((child) => {
                    child.model = value;

                    if (update) {
                        child.currentValue = value.indexOf(child.label) >= 0;
                        child.group = true;
                    }
                });
            },
            change (data) {
                this.currentValue = data;
                this.$emit('input', data);
                this.$emit('on-change', data);
                // todo 事件
//                this.$dispatch('on-form-change', data);
            }
        },
        watch: {
            value () {
                this.updateModel(true);
            }
        }
    };
</script>
