<template>
  <div class="counter">
    <textarea id="textarea" class="counter__textarea" v-model="text" @input="onTextChanged" placeholder="여기에 텍스트를 입력해주세요"></textarea>
    <label for="textarea" class="counter__label">{{ text.length }}</label>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({})
export default class App extends Vue {
  text: string = '';

  created() {
    this.text = localStorage.getItem('text') || '';
  }

  mounted() {
    window.addEventListener('beforeunload', (event: BeforeUnloadEvent) => {
      if (this.text.length === 0) return;

      event.preventDefault();
      event.returnValue = '';
    });
  }

  onTextChanged(event: any) {
    this.text = event.target.value;
    localStorage.setItem('text', event.target.value);
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.counter {
  display: flex;
  flex-direction: column;
  position: fixed;
  width: 100%;
  height: 100%;
  padding: 5px;

  &__textarea {
    height: 100%;
    padding: 10px;

    box-shadow: 1px 1px 1px #999;
    border-radius: 0;
    outline: none;

    font-size: 16px;
    color: #2c3e50;
  }
  &__label {
    align-self: flex-end;
    font-size: 26px;
  }
}
</style>
