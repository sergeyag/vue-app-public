<template>
  <v-app>

    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>КИНО</span>
        <span class="font-weight-light">Адреса</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

    </v-app-bar>

    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
    import {mapMutations} from 'vuex'

    export default {
        name: 'App',
        data () {
            return {
                drawer: false,
                links: [
                    {title: 'Home', icon: 'home', url: '/'},
                    {title: 'Список', icon: 'table', url: '/table'},
                    {title: 'Создать', icon: 'create', url: '/new'}
                ]
            }
        },
        methods: {
            loadPoints () {
                console.log("loadPoints()")
                this.$store.resource = this.$resource('http://localhost:3000/restAPI')
                this.$store.resource.get().then(response => response.json())
                    .then(points => {
                        for (var value of points) {
                            this.addPointMutation(value)
                        }
                    })
            },
            ...mapMutations(['addPointMutation', 'updatePointMutation', 'removePointsMutation'])
        },
        created () {
            console.log("created()")
            this.loadPoints()
        }
    };
</script>
