<style scoped>
    .navbar-placeholder {
        height: 100px;
    }
</style>

<template>
    <div>
        <div class="navbar navbar-default navbar-fixed-top">
            <div class="container-fluid">
                <div class="navbar-header">
                    <router-link to="/feed" class="navbar-brand">Галерея</router-link>
                </div>
                <ul class="nav navbar-nav navbar-right">
                    <li v-if="visible"><router-link to="/moderation">Модерация</router-link></li>
                    <li><router-link to="/myphoto">Мои фото</router-link></li>
                    <li><router-link to="/upload">Загрузить</router-link></li>
                    <li><a href="#" v-on:click="logOut">Выйти</a></li>
                </ul>
            </div>
        </div>
        <div class="navbar-placeholder"></div>
    </div>
</template>

<script>
    module.exports = {
        data: function() {
                return {  visible: false };
            },
        mounted: function() {
                this.$http.get("/is_moderator", { bearer: true })
                .then(function(response) {               
                    if (response.body[0].moderator != undefined) {
                        if (response.body[0].moderator == 1) {
                            this.visible = true;
                        }
                    }
                });
            },
        methods: {
            logOut: function() {
                this.$auth.logOut();
                this.$router.push("/");
            }
        }
    };
</script>
