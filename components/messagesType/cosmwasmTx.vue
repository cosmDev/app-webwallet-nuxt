<template>
  <v-container>
    <v-row class="mt-4">
      <v-spacer></v-spacer>

      <v-switch
        v-model="viewJson"
        :label="viewJson ? 'View form' : 'View json'"
      ></v-switch>
      <v-col v-if="viewJson" cols="12" sm="12" md="12">
        <vue-json-pretty
          :data="jsonData"
          show-line
          show-line-number
          show-length
          show-icon
        />
      </v-col>

      <v-col v-if="!viewJson" cols="12" sm="12" md="12">
        <v-text-field
          v-model="selectPolicy"
          label="From address"
          required
          outlined
          disabled
        ></v-text-field>
        <v-text-field
          v-model="contract"
          label="Contract address"
          required
          outlined
        ></v-text-field>
        <!--<v-text-field
          label="To validator"
          required
          outlined
        ></v-text-field>-->
        <v-text-field
          v-model="amount"
          label="Amount"
          suffix=""
          required
          outlined
        ></v-text-field>
        <v-textarea
          v-model="wasmMsg"
          outlined
          name="input-7-4"
          label="Wasm Message"
          value=""
        ></v-textarea>
      </v-col>
      <v-btn elevation="2" @click="checkMsg">Check message</v-btn>
    </v-row>
  </v-container>
</template>
<!-- <script>
import { mapState } from 'vuex'
import axios from 'axios'
import { coins } from "@cosmjs/launchpad";
import { SigningStargateClient, AminoTypes } from "@cosmjs/stargate";
import { Registry, DirectSecp256k1HdWallet } from "@cosmjs/proto-signing";
import { cosmWasmTypes, MsgExecuteContractEncodeObject } from '@cosmjs/cosmwasm-stargate';
import { toUtf8 } from '@cosmjs/encoding';

// const tx_4 = require("cosmjs-types/cosmwasm/wasm/v1/tx");
import { MsgExecuteContract, MsgStoreCode } from "cosmjs-types/cosmwasm/wasm/v1/tx";

import { cosmos, cosmosProtoRegistry, cosmosAminoConverters } from 'interchain46';
import VueJsonPretty from 'vue-json-pretty';
import 'vue-json-pretty/lib/styles.css';
import pkg from 'protobufjs';
const { Type, Field } = pkg;
import cosmosConfig from '~/cosmos.config'

  export default {
    props: ['from'],
    components: {
      VueJsonPretty,
    },
    data (props) {
      return {
        dialog: false,
        selectPolicy: props.from,
        amount: '',
        contract: '',
        wasmMsg: '',
        viewJson: false,
        jsonData: '',
        validateData: false,
        showValidateData: false,
        cosmosConfig: cosmosConfig
      }
    },
    watch: {
      from(newData, oldData) {
        this.selectPolicy = newData
      },
      viewJson(newData, oldData) {

        const executeContractMsg = {
            typeUrl: "/cosmwasm.wasm.v1.MsgExecuteContract",
            value: MsgExecuteContract.fromPartial({
                sender: this.selectPolicy,
                contract: this.contract,
                msg: (JSON.stringify(this.wasmMsg)),
                funds: [{"denom": cosmosConfig[0].coinLookup.chainDenom, "amount": this.amount}],
            }),
        };

        this.jsonData = executeContractMsg
      },
    },
    computed: {
      ...mapState('data', [`allValidators`])
    },
    methods: {
      async checkMsg() {
        this.showValidateData = true
        if (this.selectPolicy !== '' && this.toAddress !== '' && this.amount !== '' ) {
          this.validateData = true

          const MsgExecuteContractEncodeObject = {
              typeUrl: "/cosmwasm.wasm.v1.MsgExecuteContract",
              value: MsgExecuteContract.encode(MsgExecuteContract.fromPartial({
                  sender: this.selectPolicy,
                  contract: this.contract,
                  msg: toUtf8(this.wasmMsg),
                  funds: [{"denom": cosmosConfig[0].coinLookup.chainDenom, "amount": (this.amount / 1000000)}],
              })).finish()
          };

          console.log(MsgExecuteContractEncodeObject)

          await this.$store.dispatch('data/formatFinalMsgProp', MsgExecuteContractEncodeObject)
        } else
          this.validateData = false

      },
    },
    async mounted () {
      // console.log(tx_4)

    },

  }
</script>
 -->
