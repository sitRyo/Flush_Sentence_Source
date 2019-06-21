<template>
  <b-container class="wrapper">
  <div>
    <b-form-textarea
      id="textarea"
      v-model="text"
      placeholder="Enter something..."
      rows="1"
      max-rows="6"
      class="mb-3"
    ></b-form-textarea>
  </div>
  <b-row class="mb-3">
    <b-col><b-button class="weight" variant="success" @click="onClick()">Start</b-button></b-col>
    <b-col><b-button class="weight" variant="success" @click="resetSentence()">Reset</b-button></b-col>
  </b-row>
  <template v-if="isRender">
    <hr>
    <div class="weight size mb-2">{{construct}}</div>
    <b-row class="mb-3">
    <div v-for="(word, index) in words" :key="index">
      <b-col cols="2" class="mb-2"><b-button class="weight" :pressed="false" variant="info" @click="addWord(word)">{{word}}</b-button></b-col>
    </div>
    </b-row>
    <b-row>
      <b-col><b-button class="weight" variant="success" @click="judgeSentence()">Judge</b-button></b-col>
      <b-col><b-button class="weight" variant="success" @click="showAnswer()">{{message}}</b-button></b-col>
      <b-col><b-button class="weight" variant="success" @click="refreshSentence()">Refresh</b-button></b-col>
  </b-row>
  </template>
  <b-row v-show="isShow" class="answer weight mb-2 mt-2">Answer</b-row>
  <div v-show="isShow" class="weight size mt-2">{{basic}}</div>
  </b-container>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

@Component
export default class SentenceBox extends Vue {
  public text: string = "";
  public basic: string = "";
  
  public sentenseSize: number = 0;
  public isRender: boolean = false;

  public construct: string = "";

  public words: string[] = [];
  public suc: string[] = [];
  public ans: string[] = [];

  public wordInformations: {key: string, value: boolean}[] = [];

  public isShow: boolean = false;
  public message: string = "Show the Answer";

  public onClick(): void {
    if (this.text === "") {
      alert("文章を入力してください。");
      return;
    }
    this.formatArrays();
    
    
    this.text.trim();
    this.basic = this.text;
    this.suc = this.text.split(" ");
    this.words = this.suc.slice(0);
    this.sentenseSize = this.words.length;

    this.text = "";
    this.construct = "";
    this.isRender = true;

    this.words = this.shuffleSentence(this.words);
  }

  public resetSentence(): void {
    this.isRender = false;
    this.formatArrays();
  }

  public refreshSentence(): void {
    this.construct = "";
    this.ans = [];
  }

  public addWord(word: string): void {
    this.construct += word + " ";
    this.ans.push(word);
  }

  public judgeSentence(): void {
    let flag: boolean = true;
    for (let i = 0; i < this.ans.length; ++i) {
      if (this.ans[i] !== this.suc[i]) {
        flag = false;
        break;
      }
    }
    if (flag && this.ans.length === this.suc.length) {
      alert("正解！");
    } else {
      alert("不正解...");
    }
  }

  public showAnswer(): void {
    this.isShow = !(this.isShow);
    if (this.isShow) this.message = "Hide the Answer";
    else this.message = "Show the Answer"
  }

  private formatArrays(): void {
    this.words = [];
    this.suc = [];
    this.ans = [];
  }

  // Fisher-Yates Algorithm
  private shuffleSentence(words: string[]): string[] {
    const copy: string[] = [];
    let m: number = words.length;
    while (m) {
      let pick: number = Math.floor(Math.random() * m--);
      copy[m] = words[pick];
      [words[m], words[pick]] = [words[pick], words[m]];
    }
    return copy;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.weight {
  font-weight: 600;
}

.size {
  font-size: 120%;
}

.answer {
  color: #c23b22;
  font-size: 140%;
}

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
