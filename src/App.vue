<template>
  <div id="app">
    <a-row justify="center">
      <a-col :span="24">
        <a-card :title="questions[currentNum - 1].title">
          <a-progress :percent="currentNum * 100 / questions.length" :showInfo="false"/>
          <br/>
          <br/>
          <a-form
              ref="formRef"
              :model="formState"
          >
            <a-form-item name="type">
              <div v-if="questions[currentNum - 1].type === 'radio'">
                <a-radio-group v-model:value="formState.answer[currentNum - 1]">
                  <a-radio :key="index" v-for="(option,index) in questions[currentNum - 1].options" :value="option.text">
                    <img :src="option.media" />
                    {{ option.text }}
                  </a-radio>
                </a-radio-group>
              </div>
              <div v-else>
                <a-checkbox-group v-model:value="formState.answer[currentNum - 1]">
                  <a-checkbox :key="index" v-for="(option,index) in questions[currentNum - 1].options" :value="option.text"
                              name="type">
                    <img :src="option.media" />
                    {{ option.text }}
                  </a-checkbox>
                </a-checkbox-group>
              </div>
            </a-form-item>
          </a-form>
          <a-space :size="24">
            <div v-if="currentNum !== 1">
              <a-button type="primary" @click="toLastQuestion">上一题</a-button>
            </div>
            <div v-if="currentNum !== questions.length">
              <a-button type="primary" @click="toNextQuestion"
                        :disabled="formState.answer[currentNum - 1]?.length < 1 ">下一题</a-button>
            </div>
          </a-space>

        </a-card>

      </a-col>

    </a-row>


  </div>
</template>

<script>
import {reactive, ref} from "vue";
import logo from './assets/logo.png'

export default {
  name: 'App',
  components: {},
  setup() {
    const formState = reactive({
      answer: [],
    });
    const currentNum = ref(1);
    const questions = [
      {
        "title": "你知道谁是鱼皮么？",
        "options": [
          {
            media: logo,
            text: "徐州吴彦祖",
          },
          {
            media: logo,
            text: "一名程序员",
          },
          {
            media: logo,
            text: "人比头发卷",
          },
          {
            media: logo,
            text: "女装大佬",
          },
        ],
        "type": "radio" // radio 单选, checkbox 多选
      },
      {
        "title": "你知道谁是鱼皮么2？",
        "options": [
          {
            media: logo,
            text: "徐州吴彦祖",
          },
          {
            media: logo,
            text: "一名程序员",
          },
          {
            media: logo,
            text: "人比头发卷",
          },
          {
            media: logo,
            text: "女装大佬",
          },
        ],
        "type": "checkbox" // radio 单选, checkbox 多选
      },
      {
        "title": "你知道谁是鱼皮么2？",
        "options": [
          {
            media: logo,
            text: "徐州吴彦祖",
          },
          {
            media: logo,
            text: "一名程序员",
          },
          {
            media: logo,
            text: "人比头发卷",
          },
          {
            media: logo,
            text: "女装大佬",
          },
        ],
        "type": "checkbox" // radio 单选, checkbox 多选
      },
    ]
    // 上一题
    const toLastQuestion = () => {
      if (currentNum.value < 2) {
        return;
      }
      currentNum.value -= 1;
    }
    // 下一题
    const toNextQuestion = () => {
      if (currentNum.value >= questions.length) {
        return;
      }
      currentNum.value += 1;
    }
    return {
      questions,
      formState,
      currentNum,
      toNextQuestion,
      toLastQuestion,
    }
  }
}
</script>

<style>
#app {
  padding: 42px;
}
</style>
