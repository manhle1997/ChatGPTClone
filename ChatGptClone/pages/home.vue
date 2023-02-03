<template>
  <div>
    <h3>Chat GPT Clone</h3>
    <input type="text" v-model="reqMess" />
    <button @click="getResponse()">click me</button>
    <div>{{ resMess }}</div>

  </div>
</template>
<script>
export default {
  name: "Home",
  data() {
    return {
      resMess: "",
      reqMess: "",
      desImage: "",
      urlImage: "",
    };
  },
  mounted() {
    this.resMess = "Welcome to ChatGpt Clone";
  },
  methods: {
    async getResponse() {
      let url = "https://api.openai.com/v1/completions";
      let configHeader = {
          "Content-Type": "application/json",
          "Authorization":
            "Bearer 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",
      };
      let dataBody = {
          "model": "text-davinci-003",
          "prompt": "Human: "+this.reqMess,
          "temperature": 0.9,
          "max_tokens": 150,
          "top_p": 1,
          "frequency_penalty": 0,
          "presence_penalty": 0.6,
          "stop": [" Human:", " AI:"]
        };
      let res = await $fetch(url, {
        method: 'POST',
        body: dataBody,
        headers: configHeader
      });
      this.reqMess = ''
      this.resMess = res.choices[0].text
    },
  },
};
</script>
