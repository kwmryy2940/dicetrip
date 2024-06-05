<template>
  <v-container class="d-flex justify-center align-center">
    <h1>{{ title }}</h1>
  </v-container>
  <v-container class="d-flex justify-center align-center">
    <v-row dense>
      <v-col cols="12" v-for="number in 6">
        <v-card :color="colorList[number - 1]">
          <v-card-text>
            <v-text-field
              class="text-h5"
              :prepend-icon="'mdi-dice-' + number"
              variant="outlined"
              clearable
              v-model="inputValues[number - 1]"
            ></v-text-field>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
  <div class="d-flex justify-center align-center ma-2">
    <v-btn
      width="150"
      color="primary"
      prepend-icon="mdi-dice-multiple"
      @click="handleRollDice"
      >サイコロを振る</v-btn
    >
  </div>
  <div class="d-flex justify-center align-center">
    <v-btn width="150" color="red" @click="handleClearText"> クリア </v-btn>
  </div>
  <v-dialog v-model="dialog">
    <v-card>
      <v-card-text class="text-center"
        >サイコロの目:{{ diceRoll + 1 }}</v-card-text
      >
      <v-card-text class="text-center">{{ inputValues[diceRoll] }}</v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="dialog = !dialog">閉じる</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup lang="ts">
import { ref } from "vue";

defineProps<{ title: string }>();

const colorList: string[] = [
  "pink-lighten-1",
  "orange-lighten-1",
  "purple-lighten-1",
  "yellow-lighten-1",
  "blue-lighten-1",
  "light-green-lighten-1",
];

const inputValues = ref(["", "", "", "", "", ""]);
const diceRoll = ref(0);
const dialog = ref(false);

const handleRollDice = () => {
  const isEmpty = inputValues.value.some(
    (item) => item === null || item === ""
  );

  if (isEmpty) {
    alert("未入力の箇所があります");
    return;
  }

  // サイコロの出目
  diceRoll.value = Math.floor(Math.random() * 6);
  dialog.value = true;
};

const handleClearText = () => {
  for (let i = 0; i < 6; i++) {
    inputValues.value[i] = "";
  }
};
</script>
