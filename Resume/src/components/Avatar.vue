<template>
    <div class="avatar">
        <img :src="elem.text" alt="">
    </div>
</template>

<script>
export default {
    props: ['elem']
}
</script>