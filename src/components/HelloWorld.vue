<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ name }}</h1>
    <h1>{{ myArray.name }}</h1>
    <p>
      ПРИМЕР класс компонет стиля vue-class-component
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { WithRenderInterface} from "@/components/interface.HellowWorld";

@Component
export default class HelloWorld extends Vue {  
   @Prop() private msg!: string;
   @Prop() public name!: string;
   @Prop() public myArray!:WithRenderInterface 
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
