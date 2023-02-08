<script lang="ts">
export default {
    // props: {
    // },
    data() {
        return {

        }
    }
}
</script>

<template>

    <div class="todoItem row">
        <div class="circle"></div>
        <input type="text" placeholder="type ToDo here..">
    </div>
</template>

<style scoped>
.circle{
    width: 50px;
    height: 50px;
    border-radius: 100%;
    border: 1px solid var(--White-opac05);
}
</style>