<template>
<li>
    <h2>
        <a :href="artist.url" target="_blanck"> {{ artist.name }} </a>
    </h2>
    <img  :src="artist.image[2]['#text']">
</li>
</template>

<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>

<style scope>
    li {
        display: block;
        margin:  10px 0;
    }
</style>
