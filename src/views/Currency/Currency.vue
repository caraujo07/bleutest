<template >
  <div>
    <div class="intro">
      <h1>USD Best Price in Brazil</h1>
      <p>Compare and find in realtime the best effective prices in Brazil's top USD exchanges, considering fees.<br />
      <span>Click on the exchange row</span> to view opration details.</p>
    </div>
    <div v-if="loaded" class="swap">
      <div id="enabled" class="price">
        <input type="text" v-model="userValue" v-money="money" @input="updateConvertedPrice()" @keypress="onlyNumbers($event)"> 
        <select @change="onChange($event)">
          <option value="USD-BRL" selected>BRL</option>
          <option value="BRL-USD">USD</option>
        </select>
      </div>
      <div id="disabled" class="price">
        <input type="text" v-bind:value="total.toFixed(2).replace('.', ',')" disabled> 
        <select id="convertedPrice" disabled>
          <option value="USD-BRL">BRL</option>
          <option value="BRL-USD" selected>USD</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
// Importing the v-money lib to mask the first input correctly
import {VMoney} from 'v-money';

export default {
  data: function() {
    return {
      price: {},
      loaded: false,
      selectedCoin: '',
      userValue: 0,
      coinValue: 0,
      total: 0,
      money: {
        decimal: ',',
        thousands: '',
        precision: 2,
        masked: false /* doesn't work with directive */
      },
    }
  },
  directives: {money: VMoney},
  methods: {
    getPrice() {
      fetch('https://economia.awesomeapi.com.br/all/USD-BRL')
      .then(r => r.json())
      .then(r => {
        this.price = r;
        this.loaded = true;
        this.coinValue = parseFloat(this.price.USD.bid.replace(',', '.'));
      });
    },
     onChange(event) {
      this.selectedCoin = event.target.value;
      this.updateSelectedCoin();
    },
     updateSelectedCoin() {

      let valor = document.getElementById('convertedPrice');

      if(this.selectedCoin === 'USD-BRL') {
        valor.value = "BRL-USD";
      } else if(this.selectedCoin === 'BRL-USD') {
         valor.value = "USD-BRL";
      }
    },
    updateConvertedPrice() {
      let userVal = Number(this.userValue.replace(',', '.'));
    
       if(this.selectedCoin === 'USD-BRL') {
         this.total =  (userVal / this.coinValue);
      } else if(this.selectedCoin === 'BRL-USD') {
        this.total =  (userVal * this.coinValue);
       } 
    },
     onlyNumbers(e) {
      e = (e) ? e : window.event;
      let charCode = (e.which) ? e.which : e.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        e.preventDefault();
      } else {
        return true;
      }
    },
  },
  created() {
    this.selectedCoin = 'USD-BRL';
    this.getPrice();
  }
}
</script>
