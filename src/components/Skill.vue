<script>
    export default{
       props: {
            icon: {
                type: String,
                required: true
            },
    }
        
    }
</script>

<template>
    <div class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
        <img :src="icon" class="w-6 h-6" />
        <slot></slot>
    </div>
</template>