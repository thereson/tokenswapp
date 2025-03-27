<template>
    <v-app>
      <!-- Gradient Background -->
      <v-sheet
        class="gradient-background fill-height d-flex align-center justify-center"
        :style="gradientStyle"
      >
        <!-- Swap Card -->
        <v-card class="pa-6 rounded-lg" elevation="12" width="400">
          <v-card-title class="text-h4 font-weight-bold text-center mb-6">
            Swap Tokens
          </v-card-title>
  
          <!-- Input Token -->
          <v-card-text>
            <v-select
              v-model="inputToken"
              :items="tokens"
              label="From"
              outlined
              dense
              class="mb-4"
            ></v-select>
  
            <v-text-field
              v-model="inputAmount"
              label="Amount"
              type="number"
              outlined
              dense
              class="mb-4"
            ></v-text-field>
  
            <!-- Output Token -->
            <v-select
              v-model="outputToken"
              :items="tokens"
              label="To"
              outlined
              dense
              class="mb-4"
            ></v-select>
  
            <!-- Estimated Output -->
            <v-text-field
              :value="estimatedOutput"
              label="Estimated Output"
              readonly
              outlined
              dense
              class="mb-4"
            ></v-text-field>
  
            <!-- Slippage Tolerance -->
            <v-text-field
              v-model="slippage"
              label="Slippage Tolerance (%)"
              type="number"
              outlined
              dense
              class="mb-6"
            ></v-text-field>
  
            <!-- Swap Button -->
            <v-btn
              block
              color="primary"
              large
              @click="handleSwap"
            >
              Swap
            </v-btn>
          </v-card-text>
        </v-card>
      </v-sheet>
    </v-app>
  </template>
  
  <script>
  
  export default {
    data() {
      return {
        inputAmount: "", // Amount of input token
        inputToken: "BNB", // Selected input token
        outputToken: "BUSD", // Selected output token
        slippage: 1, // Slippage tolerance in percentage
        estimatedOutput: "0.0", // Estimated output amount
        tokens: ["BNB", "BUSD", "CAKE"], // List of available tokens
        gradientStyle: {
          background: "linear-gradient(270deg, #6dd5ed, #2193b0, #cc2b5e, #753a88)",
          backgroundSize: "400% 400%",
          animation: "gradientAnimation 15s ease infinite",
        },
      };
    },
    components:{
    //   toolbar
    },
    methods: {
      // Simulate fetching estimated output (replace with actual logic)
      calculateEstimatedOutput() {
        const rates = {
          BNB_BUSD: 300, // 1 BNB = 300 BUSD
          BUSD_BNB: 0.0033, // 1 BUSD = 0.0033 BNB
          BNB_CAKE: 100, // 1 BNB = 100 CAKE
          CAKE_BNB: 0.01, // 1 CAKE = 0.01 BNB
          BUSD_CAKE: 0.33, // 1 BUSD = 0.33 CAKE
          CAKE_BUSD: 3, // 1 CAKE = 3 BUSD
        };
  
        const key = `${this.inputToken}_${this.outputToken}`;
        const rate = rates[key] || 0;
        this.estimatedOutput = (this.inputAmount * rate).toFixed(2);
      },
  
      // Handle swap action
      handleSwap() {
        if (!this.inputAmount || this.inputAmount <= 0) {
          alert("Please enter a valid amount.");
          return;
        }
  
        // Simulate swap (replace with actual swap logic)
        alert(`Swapping ${this.inputAmount} ${this.inputToken} for ${this.estimatedOutput} ${this.outputToken}`);
      },
    },
    watch: {
      // Recalculate estimated output when input changes
      inputAmount() {
        this.calculateEstimatedOutput();
      },
      inputToken() {
        this.calculateEstimatedOutput();
      },
      outputToken() {
        this.calculateEstimatedOutput();
      },
    },
  };
  </script>
  
  <style>
  /* Gradient Animation */
  @keyframes gradientAnimation {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
  
  /* Apply Gradient Background */
  .gradient-background {
    min-height: 100vh;
    background: linear-gradient(270deg, #6dd5ed, #2193b0, #cc2b5e, #753a88);
    background-size: 400% 400%;
    animation: gradientAnimation 15s ease infinite;
  }
  </style>
  