  <template>
  <table class="style position">
    <tr>
      <th>Exchange</th>
      <th>volume24h</th>
      <th>volume24hTo</th>
    </tr>
    <tr v-for="(exchangeItem,index) in exchangeInfo" :key="index">
      <td>{{exchangeItem.exchange}}</td>
      <td>{{exchangeItem.volume24h}}</td>
      <td>{{exchangeItem.volume24hTo}}</td>
    </tr>
  </table>
</template>
<script>
export default {
  name: "HelloWorld",
 props: {
      exchangeInfo: Array,
    
  }
};
</script>
