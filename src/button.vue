<template>
    <button class="l-button" :class="{[`icon-${iconPosition}`]: true}">
        <l-icon class="icon" v-if="icon" :name="icon"></l-icon>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>

<script>
    import Icon from './icon'
	export default {
		props: {
			icon: {},
			iconPosition: {
				type: String,
                default: 'left',
                validator (value) {
					if (value !== 'left' && value !== 'right') {
						console.warn(`iconPosition的值为 ${value} 无法匹配`)
                		return false
                    } else {
                		return true
                    }
                }
            }
        },
        components: {Icon}
    }
</script>

<style scoped lang="scss">
    .l-button {
        vertical-align: middle;
        height: var(--button-height);
        padding: 0 1em;
        font: inherit;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex;
        justify-content: center;
        align-items: center;
        &:hover {
            border-color: var(--border-color-hover);
            position: relative;
            z-index: 1;
        }
        &:active {
            background: var(--button-active-bg);
        }
        &:focus {
            outline: none;
        }
        > .icon{
            order: 1;
            margin-right: .3em;
        }
        > .content{
            order: 2;
        }
        &.icon-left{

        }
        &.icon-right{
            > .icon{
                order: 2;
                margin-left: .3em;
                margin-right: 0;
            }
            > .content {
                order: 1;
            }
        }
    }


</style>