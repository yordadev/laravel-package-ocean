<script setup lang="ts">
import tippy from 'tippy.js'
import 'tippy.js/dist/tippy.css'
import 'tippy.js/animations/shift-away.css'

interface Props {
    content: string
    placement?: 'top' | 'bottom' | 'left' | 'right'
    theme?: 'slate' | 'amber' | 'emerald' | 'indigo'
    size?: 'small' | 'medium'
    condition?: boolean
}

const $props = withDefaults(defineProps<Props>(), {
    placement: 'bottom',
    theme: 'slate',
    size: 'medium',
    condition: true,
})

const tooltip = ref()
const tooltipInstance = ref()

onMounted(()=>{
    nextTick(() => {
        if(tooltip.value && $props.condition){
            tooltipInstance.value = tippy(tooltip.value, {
                content: $props.content,
                theme: $props.theme,
                placement: $props.placement,
                animation: 'shift-away',
                touch: 'hold',
                allowHTML: true,
                delay: 100,
            })
        }
    })
})
watch(() => $props.content, () => {
    if(tooltipInstance.value)
        tooltipInstance.value.setContent($props.content)
    
})
</script>

<template>
    <div ref="tooltip">
        <slot />
    </div>
</template>

<style>
.tippy-box[data-theme~='slate']{
    @apply bg-slate-800 rounded-full py-1 px-2 shadow-lg shadow-black/5 text-xs font-poppins text-center;
}
.tippy-box[data-theme~='slate'][data-placement^='top'] > .tippy-arrow::before{
    @apply border-t-slate-800;
}
.tippy-box[data-theme~='slate'][data-placement^='bottom'] > .tippy-arrow::before{
    @apply border-b-slate-800;
}
.tippy-box[data-theme~='slate'][data-placement^='left'] > .tippy-arrow::before{
    @apply border-l-slate-800;
}
.tippy-box[data-theme~='slate'][data-placement^='right'] > .tippy-arrow::before{
    @apply border-r-slate-800;
}

.tippy-box[data-theme~='amber']{
    @apply bg-amber-500 dark:bg-amber-600 rounded-full py-1 px-2 shadow-lg shadow-black/5 text-xs font-poppins text-center;
}
.tippy-box[data-theme~='amber'][data-placement^='top'] > .tippy-arrow::before{
    @apply border-t-amber-500 dark:border-t-amber-600;
}
.tippy-box[data-theme~='amber'][data-placement^='bottom'] > .tippy-arrow::before{
    @apply border-b-amber-500 dark:border-b-amber-600;
}
.tippy-box[data-theme~='amber'][data-placement^='left'] > .tippy-arrow::before{
    @apply border-l-amber-500 dark:border-l-amber-600;
}
.tippy-box[data-theme~='amber'][data-placement^='right'] > .tippy-arrow::before{
    @apply border-r-amber-500 dark:border-r-amber-600;
}

.tippy-box[data-theme~='emerald']{
    @apply bg-emerald-500 dark:bg-emerald-600 rounded-full py-1 px-2 shadow-lg shadow-black/5 text-xs font-poppins text-center;
}
.tippy-box[data-theme~='emerald'][data-placement^='top'] > .tippy-arrow::before{
    @apply border-t-emerald-500 dark:border-t-emerald-600;
}
.tippy-box[data-theme~='emerald'][data-placement^='bottom'] > .tippy-arrow::before{
    @apply border-b-emerald-500 dark:border-b-emerald-600;
}
.tippy-box[data-theme~='emerald'][data-placement^='left'] > .tippy-arrow::before{
    @apply border-l-emerald-500 dark:border-l-emerald-600;
}
.tippy-box[data-theme~='emerald'][data-placement^='right'] > .tippy-arrow::before{
    @apply border-r-emerald-500 dark:border-r-emerald-600;
}

.tippy-box[data-theme~='indigo']{
    @apply bg-indigo-500 dark:bg-indigo-600 rounded-full py-1 px-2 shadow-lg shadow-black/5 text-xs font-poppins text-center;
}
.tippy-box[data-theme~='indigo'][data-placement^='top'] > .tippy-arrow::before{
    @apply border-t-indigo-500 dark:border-t-indigo-600;
}
.tippy-box[data-theme~='indigo'][data-placement^='bottom'] > .tippy-arrow::before{
    @apply border-b-indigo-500 dark:border-b-indigo-600;
}
.tippy-box[data-theme~='indigo'][data-placement^='left'] > .tippy-arrow::before{
    @apply border-l-indigo-500 dark:border-l-indigo-600;
}
.tippy-box[data-theme~='indigo'][data-placement^='right'] > .tippy-arrow::before{
    @apply border-r-indigo-500 dark:border-r-indigo-600;
}
</style>