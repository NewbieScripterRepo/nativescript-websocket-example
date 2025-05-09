<script lang="ts" setup>
import { ref } from 'nativescript-vue';
let ws: WebSocket | null = null;
const wsReady = ref(false);
const message = ref('');
const messages = ref<string[]>([]);

function connect() {
  ws = new WebSocket('wss://echo.websocket.org/');
  ws.onopen = () => {
    console.log('WebSocket is open');
    wsReady.value = true;
  };
  ws.onmessage = (event: MessageEvent) => {
    console.log('WebSocket message received:', event.data);
    messages.value.push("[RECEIVED] " + event.data);
  };
  ws.onerror = (event: Event) => {
    console.log('WebSocket error:', event);
  };
}
function sendMessage() {
  ws?.send(message.value);
  messages.value.push("[SENT] " + message.value);
  message.value = '';
}
function disconnect() {
  ws?.close();
  wsReady.value = false;
}
</script>

<template>
  <Frame>
    <Page>
      <ActionBar>
        <Label text="Home" class="font-bold text-lg" />
      </ActionBar>

      <GridLayout v-if="!wsReady"  rows="*, auto, auto, *" class="px-4">
        <Button
          row="2"
          @tap="connect"
          class="mt-4 px-4 py-2 bg-white border-2 border-blue-400 rounded-lg"
          horizontalAlignment="center"
        >
          Connect
        </Button>
      </GridLayout>
      <GridLayout v-else rows="60, auto, auto, *" columns="*, 5, 120" class="px-4 w-full">
        <TextField
          row="1"
          col="0"
          v-model="message"
          class="mt-4 px-4 py-2 bg-white border-2 border-blue-400 rounded-lg w-full"
          horizontalAlignment="center"
        />
        <Button
          row="1"
          col="2"
          @tap="sendMessage"
          class="mt-4 px-4 py-2 bg-white border-2 border-blue-400 rounded-lg w-full"
          horizontalAlignment="center"
        >
          Send
        </Button>
        <Button
          row="2"
          col="2"
          @tap="disconnect"
          class="mt-4 px-4 py-2 bg-white border-2 border-blue-400 rounded-lg w-full"
          horizontalAlignment="center"
        >
          Disconnect
        </Button>
        <TextView
          row="3"
          col="0"
          colSpan="3"
          class="mt-4 px-4 py-2 bg-white border-2 border-blue-400 rounded-lg"
          :text="messages.join('\n')"
        />
      </GridLayout>
    </Page>
  </Frame>
</template>

<style>
/* .info {
    font-size: 20;
  } */
</style>
