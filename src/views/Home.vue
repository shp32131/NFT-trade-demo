<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo-ether.png">
    <button @click="getProxy">getProxy</button>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import HelloWorld from '@/components/HelloWorld.vue' // @ is an alias to /src

import Web3 from 'web3'
import { OpenSeaPort, Network } from 'opensea-js'

@Options({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  // This example provider won't let you make transactions, only read-only calls:
  public providerReadonly: any
  public musicy: any
  public accountAddress = ''

  created (): void {
    this.accountAddress = '0x69053524Dacecd62bd71D2b6Dfd797afA3518bBB'
  }

  mounted (): void {
    this.providerReadonly = new Web3.providers.HttpProvider('https://rinkeby.infura.io/v3/667a42d466ba45e1ac6bdc4ae25fdd73')
    this.musicy = new OpenSeaPort(this.providerReadonly, {
      networkName: Network.Rinkeby,
      apiKey: 'efbd09f6acbd4cefa5f2bb8b424063f2'
    })
  }

  /**
   * @function getProxy
   * @param { accountAddress }
   * @returns
  */
  async getProxy (): Promise<string> {
    const proxy = await this.musicy._wyvernProtocol.wyvernProxyRegistry.proxies.callAsync(this.accountAddress)
    console.log(proxy)
    return proxy
  }

  /**
   * @function
  */
  createSellOrder (): void {
    console.log('creat sell order')
  }

  /**
   * @function createBuyOrder
  */
  createBuyOrder (): void {
    console.log('create buy order ')
  }

  /**
   * @function orderMatch
  */
  orderMatch (): void {
    console.log('order match')
  }
}
</script>
