<template>
  <div>
    <v-ons-navigator :page-stack="pageStack">
      <component :is="page" v-for="page in pageStack" :page-stack="pageStack" :txs="txs" v-on:create="addTx" v-on:deleteAll="deleteAllTx" v-on:delete=deleteTx></component>
    </v-ons-navigator>
</div>
</template>

<script>
  import page1 from './Page1';
  import page2 from './Page2';

  export default {
    data() {
      return {
        pageStack: [page1],
        txs: [],
      }
    },
    watch: {
      txs: {
        handler: function () {
          localStorage.setItem('txs', JSON.stringify(this.txs));
        },
        deep: true,
      }
    },
    mounted: function () {
      this.txs = JSON.parse(localStorage.getItem('txs')) || [];
    },
    methods: {
      addTx: function (tx) {
        this.txs.push(tx);
      },
      deleteTx: function (index) {33
        if (confirm('この支払い履歴を削除しますか？')) {
          this.txs.splice(index, 1);
        }
      },
      deleteAllTx: function () {
        if (!confirm("本当にちゃんと渡した？")) {
          return;
        }
        this.txs = [];
      }
    },
  }
</script>
