<template>
  <v-ons-page>
    <custom-toolbar :back-label="'Page 1'">新しい支払い</custom-toolbar>
    <v-ons-list>

      <v-ons-list-item>
        <div class="center">
          <v-ons-input type="number" placeholder="ユーザーID" float
            v-model="newUserId"
          >
          </v-ons-input>
        </div>
      </v-ons-list-item>
      <v-ons-list-item>
        <div class="center">
          <v-ons-input type="number" placeholder="金額" float
            v-model="newAmount"
          >
          </v-ons-input>
        </div>
      </v-ons-list-item>
    </v-ons-list>
    <p style="text-align: center">
      <v-ons-button style="margin: 6px 0" @click="create">決定</v-ons-button>
    </p>


<!--
    <v-ons-list>
      <v-ons-list-item tappable>
        <label class="left">
          <v-ons-radio v-model="newUserId" :value=0 :input-id="radio-1"></v-ons-radio>
        </label>
        <label :for="radio-1" class="center">
          えの
        </label>
      </v-ons-list-item>
      <v-ons-list-item tappable>
        <label class="left">
          <v-ons-radio v-model="newUserId" :value=1 :input-id="radio-2"></v-ons-radio>
        </label>
        <label :for="radio-2" class="center">
          かみ
        </label>
      </v-ons-list-item>
    </v-ons-list>
-->



  </v-ons-page>
</template>


<script>
  import customToolbar from './CustomToolbar';
  import app from './App';

  export default {
    data() {
      return {
        newUserId: 0,
        newAmount: 0
      }
    },
    methods: {
      pop() {
        this.pageStack.pop();
      },
      create() {
        var tx = {
          userId: this.newUserId,
          amount: this.newAmount
        };
        this.$emit('create', tx);
        this.pop();
      }
    },
    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
