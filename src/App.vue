<template>
  <div>
    <News />
  </div>
</template>

<script>
import News from './components/News.vue'
import MeiZi from './components/MeiZi.vue'

export default {
  name: 'app',
  components: {
      News,
      MeiZi
  }
}
</script>

<style>

    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    html,body{
        width: 100%;
        height: 100%;
    }

</style>
