<template xmlns:v-on="http://www.w3.org/1999/xhtml">
  <div>

    <table>
      <tr>
        <th>ID</th>
        <td>Name</td>
        <td>GOLD</td>
        <td>USD</td>
      </tr>

      <tr v-for="account in accounts">
        <td> {{account.id}}</td>
        <td> {{account.username}}</td>
        <td> {{account.goldBalance}}</td>
        <td> {{account.usdBalance}}</td>
      </tr>
    </table>

    <button v-on:click="getAccount">查询账户</button>

  </div>
</template>

<script>
  export default {
    name: 'account',
    data() {
      return {
        accounts: [
          {
            id: 1,
            username: 'Jack',
            usdBalance: 100,
            goldBalance: 200
          },
          {
            id: 2,
            username: 'Tom',
            usdBalance: 20,
            goldBalance: 50
          },
        ]
      }
    },
    methods: {
      getAccount: function () {
        this.$http.post('http://localhost:3000/api', {
          jsonrpc: '2.0',
          id: 1,
          method: 'query',
          params: ["demo.gp.GPContract", "accounts", ""]
        }, {headers: {}}).then(response => {
          console.log(response.body);
          this.accounts = response.body;
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
