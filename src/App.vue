<template>
  <div id="app">
    <main role="main">

      <!-- Main jumbotron for a primary marketing message or call to action -->
      <div class="jumbotron custom-jumbotron">
        <div class="row justify-content-center">
          <div class="col-6">
            <form  v-on:submit.prevent action="" class="form">
              <div class="form-group">
                <label for="numbers">Quantity</label>
                <input v-model="quantity" type="text" class="form-control" id="numbers" placeholder="">
              </div>
              <div class="form-group">
                <input type="submit" @click="generateNumbers" class="btn btn-default" value="Generate">
                <input type="submit" @click="clear" class="btn btn-info" value="Clear">
              </div>
            </form>
          </div>
        </div>
      </div>

      <div class="container">
        <!-- Example row of columns -->
        <div class="row">
          <div class="col-12">
            <transition-group name="list" tag="div" class="row">
              <div class="col-3 single" :key="index" v-for="(number, index) in sorted">
                <p class="number"> {{ (index + 1) }} <i class="fas fa-long-arrow-alt-right"></i>   {{ number }} </p>
              </div>
            </transition-group>
          </div>

        </div>
      </div> <!-- /container -->

    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      quantity : '',
      numbers: [],
      sorted: [],
      hasGenerate: false
    }
  },
  methods: {
    generateNumbers(){
      this.sorted = [];
      this.numbers = Array.from({length: this.quantity}).map( (e,i) => i + 1 );
      this.hasGenerate = true;

      let startingLength = this.numbers.length;
      let i = 0;

      for( i= 0 ; i < startingLength; i++){
        let random = Math.floor( Math.random() * this.numbers.length);
        let current = this.numbers.splice( random , 1);
        setTimeout( () => {
          this.sorted.push(current[0]);
        }, i * 200)
      }
    },
    clear(){
      this.numbers = [];
      this.sorted = [];
      this.quantity = "";
      this.hasGenerate = false;
    },
  }
}
</script>

<style lang="scss">
  .number {
    cursor:default;
    text-align: center;
    color: white;
    font-size: 50px;
  }

  .custom-jumbotron {
    height: 170px !important;
    padding: 0px !important;
    padding-top: 20px !important;
  }

  .single {
    background-color: #007bff;
    border: 1px solid #FFFFFF;
  }

  i {
    font-family:  FontAwesome;
    font-style: normal;
  }

  .list-item {
    display: inline-block;
    margin-right: 10px;
  }
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
  }



</style>
