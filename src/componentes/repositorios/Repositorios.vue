<template>
    <section class="main">
        <h1> Lista de repositorios </h1>
        <ul>
            <li v-for="repositorio in repositorios">
                <p>{{repositorio.name}}</p>
            </li>
        </ul>        
    </section>
</template>

<script>
export default {

    props: ['repositorios'],

    data() {
        return {
            
        }
    }
}
</script>

<style scope>
    body{
        margin: 0;
        overflow-y: hidden;
    }
    ul, li{
        list-style: none;
        margin: 1px 0;
        padding: 0;
        border-bottom: 1px solid #9c27b0;
    }
    .main{
        background-color: #F6F9FA;
        height: 100vh;
        max-height: 100%;
        position: absolute;
        right: 0;
        left: 260px;
        padding: 0% 10%;
        overflow-y: auto; 
    }
</style>
