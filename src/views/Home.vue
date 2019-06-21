<template>
  <div class="home">
    <SentenceBox></SentenceBox>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SentenceBox from '@/components/SentenceBox.vue'; // @ is an alias to /src

@Component({
  components: {
    SentenceBox,
  },
})
export default class Home extends Vue {}
</script>
