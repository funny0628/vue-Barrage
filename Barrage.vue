<template>
  <div class="content">
    <div class="topShow">
      <div :class="{ right: showValue }" :style="{ color: randomColor() }">
        {{ showValue }}
      </div>
    </div>
    <div class="bottomInput">
      <quillEditor
        class="text"
        v-model="content"
        ref="myQuillEditor"
        :options="editorOption"
        @blur="onEditorBlur($event)"
        @focus="onEditorFocus($event)"
        @ready="onEditorReady($event)"
      ></quillEditor>
      <div class="img">
        <img @click="toShowEmoji()" src="../../Demoimg/Emoji.png" alt="" />
        <div class="Emoji-List" v-show="Emoji">
          <img
            v-for="(val, name) in list"
            :key="name"
            :src="'./emjoy/' + val + '@2x.png'"
            @click="getEmoji(val)"
          />
        </div>
      </div>
      <input @click="toSend()" class="button" type="button" value="发送" />
    </div>
  </div>
</template>

<script>
import EmojiList from "./Emoji.js";
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";

import { quillEditor } from "vue-quill-editor";
export default {
  components: {
    quillEditor
  },
  data() {
    return {
      content: '<h2>I am Example</h2>',
      //用户的输入
      userInput: "",
      //显示在窗口的文本
      showValue: "",
      Emoji: false,
      list: EmojiList
    };
  },
  methods: {
    //发送文本
    toSend() {
      this.showValue = this.userInput;
      this.userInput = "";
    },
    toShowEmoji() {
      this.Emoji = !this.Emoji;
    },
    //点击表情
    getEmoji(val) {
      window.console.log(val);
      this.userInput += `<img src="./emjoy/${val}@2x.png">`;
    },

    //随机颜色
    randomColor() {
      let r = Math.floor(Math.random() * 256);
      let g = Math.floor(Math.random() * 256);
      let b = Math.floor(Math.random() * 256);
      let rgb = `rgb(${r},${g},${b})`;
      return rgb;
    }
  },
  created() {
    window.console.log(EmojiList);
    let newList = {};
    for (var item in EmojiList) {
      newList[item] = EmojiList[item];
    }
    window.console.log(newList);

    this.list = newList;
  }
};
</script>

<style lang="less">
@import url("./Barrage.less");
</style>
