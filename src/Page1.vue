<template>
  <v-ons-page>
    <custom-toolbar>2人用割り勘アプリ</custom-toolbar>
    <v-ons-card>
      <div class="title">
        <div style="text-align: center">
          <span v-if="this.diffAmount == 0">
            貸し借りはないよ～<br>
          </span>
          <span v-else>
            <span v-if="this.diffAmount > 0">
              えのは{{Math.round(diffAmount/2)}}円わたしてね<br>
            </span>
            <span v-else>
              かみは{{Math.round(-diffAmount/2)}}円わたしてね<br>
            </span>
          </span>
        </div>
      </div>
      <div class="content">
        <p style="text-align: center">
          かみが払った額 : {{myTotalAmount}}円<br>
          えのが払った額 : {{yourTotalAmount}}円
        </p>
        <p style="text-align: center">
          <v-ons-button style="margin: 6px 0" @click="deleteAll">清算した</v-ons-button>
        </p>
      </div>
    </v-ons-card>

    <v-ons-list modifier="inset">
      <v-ons-list-header>支払い履歴</v-ons-list-header>
      <div v-if="this.txs.length">
        <div v-for="(tx,index) in this.txs">
          <v-ons-list-item modifier="longdivider">
              <span @click="$emit('delete',index)">x　　</span>
              ID : {{tx.userId}} : {{ tx.amount }} 円
          </v-ons-list-item>
        </div>
      </div>
      <div v-else>
        <v-ons-list-item  modifier="longdivider">支払い履歴はないよ～</v-ons-list-item>
      </div>
    </v-ons-list>



    <v-ons-fab
      position="bottom right"
      @click="push"
    >
      <v-ons-icon icon="md-plus"></v-ons-icon>
    </v-ons-fab>
  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import page2 from './Page2';
  export default {
     methods: {
       pop(){
         this.pageStack.pop();
       },
       push() {
         this.pageStack.push(page2);
       },
       deleteAll(){
        this.$emit('deleteAll');
       }
     },
     computed: {
       myTotalAmount: function(){
         return this.txs.reduce(function (sum, tx) {
           if (tx.userId == 0) return sum + Number(tx.amount);
           return sum;
         }, 0);
       },
       yourTotalAmount: function(){
         return this.txs.reduce(function (sum, tx) {
           if (tx.userId == 1) return sum + Number(tx.amount);
           return sum;
         }, 0);
       },
       diffAmount: function(){
          return this.myTotalAmount - this.yourTotalAmount;
       }
     },
     props: ['pageStack','txs'],
     components: { customToolbar }
  }
</script>
