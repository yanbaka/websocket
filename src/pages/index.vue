<template>
  <div>
    <input type="button" value="送信" @click="send">
    <ul>
      <li v-for="(message, key) in messages" :key="key">
        {{ message }}
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  data () {
    return {
      ws: null,
      messages: []
    }
  },
  mounted() {
    // WebSocketのクライアントの生成
    this.ws = new WebSocket('ws://localhost:5001')

    // 接続時に呼ばれる
    this.ws.addEventListener('open', e => {
        console.log('open')
    })

    // サーバからのデータ受信時に呼ばれる
    this.ws.addEventListener('message', e => {
        console.log(e.data)
        this.messages.push(e.data)
    })

  },
  methods: {
    send() {
      this.ws.send('hello')
    }
  }
}
</script>