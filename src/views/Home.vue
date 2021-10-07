<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld :myArray="{name:5}" name="HEllow world" msg="Welcome !!!!!!!!!!!!!!!!!!" />
    <MyComponent :message="{title:'Hellow World from my component'}"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import MyComponent from "@/components/MyComponent.vue"

@Component({
  components: {
    HelloWorld,
     MyComponent
  },
})
export default class Home extends Vue {
  
}
</script>
