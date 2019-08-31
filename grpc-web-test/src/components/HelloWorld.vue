<template>
  <div id='app'>
    <section>
      <span class='title-text'>gRPC Client</span>
      <div class='row justify-content-center mt-4'>
        <input v-model='inputField' v-on:keyup.enter='addNum' class='mr-1' placeholder='Please input Number'>
        <button @click='addNum' class='btn btn-primary'>Add Num</button>
      </div>
    </section>
    <section>
      <h2>now total: {{num.total}}</h2>
    </section>
  </div>
</template>

<script>
import { HelloRequest } from '../grpc/helloworld_pb'
import { GreeterClient } from '../grpc/helloworld_grpc_web_pb'
export default {
  name: 'app',
  components: {},
  data: function () {
    return {
      inputField: '',
      num: 0
    }
  },
  created: function () {
    // eslint-disable-next-line
    this.client = new GreeterClient('http://localhost:8001', null, null)
    this.sayHello()
    
  },
  methods: {
    sayHello: function () {
      // eslint-disable-next-line
      let getRequest = new HelloRequest()
      getRequest.setName("きり丸");
      // eslint-disable-next-line
      this.client.sayHello(getRequest, {}, (err, response) => {
        this.num = response.toObject()
        console.log(this.num)
      })
    },
    // addNum: function () {
    //   // eslint-disable-next-line
    //   let request = new addNumParams()
    //   request.setNumber(Number(this.inputField))
    //   // eslint-disable-next-line
    //   this.client.addNum(request, {}, (err, response) => {
    //     this.inputField = ''
    //     this.num = response.toObject()
    //   })
    // }
  }
}
</script>