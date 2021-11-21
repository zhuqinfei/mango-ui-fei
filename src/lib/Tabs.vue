<template>
    <div class="mango-tabs">
        <div class="mango-tabs-nav">
           <div class="mango-tabs-nav-item" 
             v-for="(t,index) in titles" 
             @click="select(t)" 
             :class="{selected: t=== selected}" 
             :key="index">{{t}}
           </div>
        </div>
        <div class="mango-tabs-content">
            {{ current }}
            <component class="mango-tabs-content-item" :is="current" />
        </div>
    </div>
</template>

<script lang="ts">
import Tab from './Tab.vue'
import { computed } from 'vue'

export default {
    props: {
        selected: {
            type: String,
        }
    },
    setup(props, context) {
        const defaults = context.slots.default()
        defaults.forEach((tag) => {
            if (tag.type !== Tab) {
                throw new Error('Tab 子标签必须是 Tab')
            }
        })
        const current = computed(() => {
            console.log('重新 return')
            return defaults.filter((tag) => {
                return tag.props.title === props.selected
            })[0]
        })
        const titles = defaults.map((tag) => {
            return tag.props.title
        })
        const select = (title: string) => {
            context.emit('update:selected', title)
        }
        return { defaults, titles,current,select }
    }
}
</script>

<style lang="scss">
$blue: #40a9ff;
$color: #333;
$border-color: #d9d9d9;
.mango-tabs {
    &-nav {
        display: flex;
        color: $color;
        border-bottom: 1px solid $border-color;
        &-item {
            padding: 8px 0;
            margin: 0 16px;
            cursor: pointer;
            &:first-child {
                margin-left: 0;
            }
            &.selected {
                color: $blue;
            }
        }
    }
    &-content {
        padding: 8px 0;
    }
}
</style>