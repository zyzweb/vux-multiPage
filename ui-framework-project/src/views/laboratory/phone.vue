<template>
  	<div>
		<group>
		    <x-input title="手机号码" v-model="phone"></x-input>
		</group>
		<div class="btn-padding">
			<x-button type="primary" @click.native="startTest">开始查询</x-button>
		</div>
		<group>
                  <p>{{`城市:&nbsp&nbsp&nbsp${data.city}`}}</p>
                  <p>{{`运营商:&nbsp&nbsp&nbsp ${data.company}`}}</p>
                  <p>{{`省份:&nbsp&nbsp&nbsp ${data.province}`}}</p>
	    </group>
    </div>
</template>

<script>
import { XInput, Group, XButton, XTextarea, Panel } from 'vux'
import { getPhone } from '_ser/moduleB'

export default {
	data() {
		return {
			phone: '13478567723',
			data: {
                city:'',
                company:'',
                province:'',
            }
		}
    },
    mounted() {
        this.startTest()
    },
	methods: {
		startTest() {
			getPhone({
				phone: this.phone,
				key: '2dfd99df96aa125d2c2f9aa4b14daaa2', // 填写你自己的 AppKey
			}).then(response => {
				if (!response.error_code) {
					this.data = response.result

					
				}	
			})
		}
	},
  	components: {
   	 	XInput,
   	 	XButton,
    	Group,
        XTextarea,
        Panel
  	},
}
</script>

<style scoped>
.btn-padding {
	padding: 15px;
}
</style>