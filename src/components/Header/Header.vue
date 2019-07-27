<template>
  <div class="header">
    <nav>
      <router-link to="/"><img src="../../assets/logo.png" alt="Bleutest"></router-link>
      <div class="nav">
        <ul>
          <li><router-link to="/buy">Bleutest BUY</router-link></li>
          <li><router-link to="/compare">Compare</router-link></li>
          <li><router-link to="/remittance">Remittance</router-link></li>
          <li><router-link to="/exchanges">Exchanges</router-link></li>
          <li><router-link to="/exchanges-free">Exchanges' free</router-link></li>
      </ul>
      <button class="btn">Login</button>
      <div class="country">
        <span v-if="brl"><img src="../../assets/brl.png" alt="Brasil"></span>
        <span v-if="usd"><img src="../../assets/usd.png" alt="Estados Unidos da América"></span>
        <select id="lang" @change="flagChange($event)">
          <option value="BRL" selected>BRL</option>
          <option value="USD">USD</option>
        </select>
      </div>
    </div>
    <div id="toggle">
      <div id="nav-btn" @click="slideToggle()">
        <div></div>
        <div></div>
        <div></div>
      </div>
      <section id="nav-slide">
        <ul>
          <li><router-link to="/buy">Bleutest BUY</router-link></li>
          <li><router-link to="/compare">Compare</router-link></li>
          <li><router-link to="/remittance">Remittance</router-link></li>
          <li><router-link to="/exchanges">Exchanges</router-link></li>
          <li><router-link to="/exchanges-free">Exchanges' free</router-link></li>
      </ul>
      </section>
    </div>
    </nav>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      flag: '',
      brl: true,
      usd: false
    }
  },
  methods: {
    flagChange(event) {
      this.flag = event.target.value;
      if(this.flag === 'BRL') {
        this.brl = true;
        this.usd = false;
      } else if (this.flag === 'USD') {
        this.brl = false;
        this.usd = true;
      }
    },
    slideToggle() {
      let slider = document.getElementById('nav-slide');
      slider.style.height = window.innerHeight - 60 + 'px';

      if(slider.style.left == '0px') {
        slider.style.left = '-250px';
      }else {
        slider.style.left = '0px';
      }
    }   
  }
}
</script>
