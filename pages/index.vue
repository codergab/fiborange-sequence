<template>
  <div class="columns is-centered">
    <div class="column is-one-third">
      <div class="card">
        <h3 class="card-header-title">Fibonacci Range Calculator</h3>
      </div>
      <div class="card-content" style="background-color: #fff">
        <!-- Alerts -->
        <div v-if="showAlert">
          <article class="message" :class="isValid ? 'is-success':'is-warning'">
            <div class="message-header">
              {{ isValid ? `Number is valid!` : `Number is invalid!` }}
              <button
                class="delete"
                aria-label="delete"
              ></button>
            </div>
          </article>
        </div>
        <div class="card-text">
          <div class="columns">
            <div class="column is-12">
              <div class="field">
                <div class="control">
                  <label class="label is-pulled-left">Maximum Number</label>
                  <input class="input" type="number" v-model="numbers.maximum">
                </div>
              </div>
            </div>
          </div>
          <div class="columns">
            <div class="column is-6">
              <div class="field">
                <div class="control">
                  <label class="label is-pulled-left">Random Number</label>
                  <input class="input" type="number" v-model="numbers.random">
                </div>
              </div>
            </div>
            <div class="column is-4">
              <button
                style="margin-top: 2em"
                class="button is-block is-info"
                @click="computeResult('validate')"
              >Add to Sequence</button>
            </div>
          </div>

          <div v-if="showResult" class="columns">
            <div class="column is-12">
              <div>
                <h4>Fibonacci Result Computed</h4>
                <span
                  class="tag is-link"
                  v-for="(number, index) in numbers.result"
                  :key="index"
                >{{ number}}</span>&nbsp;&nbsp;
              </div>
            </div>
          </div>
          <div class="columns">
            <div class="column is-12 has-text-centered">
              <div class="control">
                <button class="button is-success" @click="computeResult('compute')">Compute</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  },
  data() {
    return {
      showResult: false,
      numbers: {
        random: 0,
        maximum: 0,
        result: []
      },
      isValid: false,
      showAlert: false
    };
  },
  methods: {
    computeResult(type) {
      let init = 0;
      let current = 1;
      let next = 0;
      let max = this.numbers.maximum;
      this.numbers.result.length = 0;
      for (let i = 0; i < max; i++) {
        this.numbers.result.push(init);
        next = init + current;
        init = current;
        current = next;
      }
      if (type == "validate") {
        this.showResult = false;
        if (this.numbers.result.includes(Number(this.numbers.random))) {
          this.isValid = true;
          this.showAlert = true;
        } else {
          this.isValid = false;
          this.showAlert = true;
        }
        // this.numbers.random = "";
        // console.log(this.numbers.result);
      } else {
        if (this.numbers.result.length > 0) {
          this.showResult = true;
        } else {
          alert("Please Set a Maximum Number");
        }
      }
    }
  },
  mounted() {}
};
</script>
