<template>
  <div class="home">
    <div class="box">
      <div class="box-left">
        <div class="box-left_back">
          <div class="box-left_back_icon">
            <img src="../assets/left-arrow.png" width="25"/>
          </div>
          <div class="box-left_back_text">
            <span>Back to cart</span>
          </div>
        </div>
        <div class="box-left_title">
          <span>Delivery details</span>
        </div>
        <div class="box-left_input">
          <div class="box-left_input_email">
            <input v-validate="'email'" type="text" placeholder="Email" name="email">
            <br/>
            <span>{{ errors.first('email') }}</span>
          </div>
          <div class="box-left_input_phone">
            <input type="text" placeholder="Phone Number">
          </div>
          <div class="box-left_input_address">
            <p>Total Remaining: <span v-bind:class="{'text-danger': errMsg }">{{totalRemainCount}}</span></p>
            <textarea placeholder="Address"
                      v-validate="'required'"
                      name="address"
                      v-on:keyup="liveCountDown"
                      v-model="address"></textarea>
            <br/>
            <span>{{ errors.first('address') }}</span>
          </div>
        </div>
      </div>
      <div class="box-middle">
        <div class="box-middle_checkbox_wrapper">
          <input type="checkbox" v-model="checked" value="dropshipper" /> Send as dropshipper
        </div>
        <div class="box-middle_input" v-if="checked === true">
          <div class="box-middle_input_drop_name">
            <input type="text" placeholder="Dropshipper name" />
          </div>
          <div class="box-middle_input_drop_phone_number">
            <input type="text" placeholder="Dropshipper phone number" />
          </div>
        </div>
        <div class="box-middle_input" v-else>
          <div class="box-middle_input_drop_name">
            <input type="text" placeholder="Dropshipper name" disabled />
          </div>
          <div class="box-middle_input_drop_phone_number">
            <input type="text" placeholder="Dropshipper phone number" disabled />
          </div>
        </div>
      </div>
      <div class="box-right">
        <div class="box-right_container">
          <div class="box-right_vl"></div>
          <div class="box-right_right_side">
            <div class="box-right_title">
              <div class="box-right_title_text">
                <span>Summary</span>
              </div>
              <div class="box-right_title_item">
                <span>10 items purchsed</span>
              </div>
              <div class="box-right_price">
                  <div class="box-right_price_goods">
                    <div class="box-right_price_goods_text">
                      <span>Cost of goods</span>
                    </div>
                    <div class="box-right_price_goods_number">
                      <span><strong>{{price.toLocaleString('en-US')}}</strong></span>
                    </div>
                  </div>
                  <div class="box-right_drop_fee">
                    <div class="box-right_drop_fee_text">
                      <span>Dropshipping Fee</span>
                    </div>
                    <div class="box-right_drop_fee_text_number" v-if="dropShipFee() > 0">
                      <span><strong>{{dropShipFee().toLocaleString('en-US')}}</strong></span>
                    </div>
                     <div class="box-right_drop_fee_text_number_zero" v-else-if="dropShipFee() === 0">
                      <span><strong>{{dropShipFee().toLocaleString('en-US')}}</strong></span>
                    </div>
                  </div>
                  <div class="box-right_total">
                    <div class="box-right_total_text">
                      <span>Total</span>
                    </div>
                    <div class="box-right_total_number">
                      <span>{{total()}}</span>
                    </div>
                  </div>
                  <div class="box-right_btn">
                    <button class="btn_submit"> Continue to Payment </button>
                  </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Home',
  data () {
    return {
      checked: false,
      price: 500000,
      limitMaxCount: 120,
      totalRemainCount: 120,
      errMsg: false,
      address: ''
    }
  },
  methods: {
    total () {
      const total = this.price + this.dropShipFee()
      return total.toLocaleString('en-US')
    },
    dropShipFee () {
      if (this.checked === false) {
        console.log(this.checked)
        return 0
      } else {
        return 5900
      }
    },
    liveCountDown () {
      this.totalRemainCount = this.limitMaxCount - this.address.length
      this.errMsg = this.totalRemainCount < 0
    }
  }
}
</script>
<style>
.box {
  width: 80%;
  height: 600px;
  background-color: white;
  margin-left: auto;
  margin-right: auto;
  display: flex;
}
.box-left{
  width: 46%;
}
.box-middle{
   width: 33%;
}
.box-right{
  width: 33%;
}
.box-left_back {
  display: flex;
}
.box-left_back_icon{
  margin-left: 50px;
  margin-top: 40px;
}
.box-left_back_text {
  margin-left: 20px;
  margin-top: 40px;
}
.box-left_title {
  margin-top: 20px;
  font-size: 40px;
  color: #FF8A00;
  font-weight: 900;
}
.box-left_input {
  margin-left: 45px;
  margin-top: 15px;
}
.box-left_input_email input[type=text],.box-left_input_phone  input[type=text], select {
  width: 400px;
  padding: 12px 20px;
  margin: 5px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  height: 60px;
}
textarea{
  outline: none;
  resize: none;
  width: 400px;
  padding: 12px 20px;
  margin: 5px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  height: 120px;
}
.box-middle_input {
  margin-top: 30px;
}
.box-middle_checkbox_wrapper {
  margin-left: 100px;
  margin-top: 110px;
}
.box-middle_input_drop_name input[type='text'], .box-middle_input_drop_phone_number input[type='text'] {
  width: 300px;
  padding: 12px 20px;
  margin: 5px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  height: 60px;
}
.box-right_vl {
  width: 1px;
  height: 510px;
  background: #FF8A00;
  opacity: 0.2;
  margin-top: 80px;
}
.box-right_container {
  display: flex;
}
.box-right_right_side {
  display: flex;
  flex-direction: column;
}
.box-right_title {
  margin-top: 105px;
}
.box-right_title_text {
  margin-left: -180px;
}
.box-right_title_text span {
  font-size: 24px;
  font-weight: 700;
  color: #FF8A00;
}
.box-right_title_item {
  margin-left: -160px;
  font-size: 15px;
}
.box-right_price {
  margin-top: 250px;
  margin-left: 10px;
}
.box-right_price_drop_fee {
  margin-top: 8px;
  margin-left: 30px
}
.box-right_price_goods {
  display: flex;
}
.box-right_price_goods_number {
  margin-left: 150px;
}
.box-right_drop_fee {
  display: flex;
}
.box-right_drop_fee_text_number {
  margin-left: 142px;
}
.box-right_drop_fee_text_number_zero {
  margin-left: 175px;
}
.box-right_total {
  display: flex;
  margin-top: 15px;
  margin-bottom: 15px;
  font-size: 24px;
  font-weight: 700;
  color: #FF8A00
}
.box-right_total_number {
  margin-left: 170px;
}
.btn_submit {
  width: 320px;
  height: 60px;
  background-color: #FF8A00;
  color: #ffff;
  border: none;
}
</style>
