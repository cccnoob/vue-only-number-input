<!-- onlynumberinput -->
<template>
  <input type="text" v-bind:value="value" v-on:input="cinput($event)" v-on:change="$emit('change')">
</template>

<script>

export default {
	props:{
		value:{
			default:'',
		},
		decimal:{
			default:0
		},
		max:{
			default:0
		}
	},
  data () {
    return {
        newVal:'',
    };
  },
	created(){
		this.initVal();
	},
	watch:{
		decimal:function(){
			this.initVal();
		}
	},
  mounted: function(){
		
	},
  methods: {
			initVal(){
				this.newVal =  this.onlyNum(this.value,this.decimal) ;
				this.$emit('input', this.newVal);
			},
      cinput(e){
					var val = event.target.value;
					if(this.max && val > this.max){
						e.target.value = this.max;
					}else{
						e.target.value = this.onlyNum(val,this.decimal);
					}
          this.$emit('input', e.target.value);
			},
			onlyNum(val,size){
					val = String(val);
					val = val.replace(/^0+/, "0");
					if(size == 0 || !size){
							val = val.replace(/[^\d]/g, "");
							if(val > 0){
								val = Number(val);
							}
					}else{
							var reg = new RegExp("^(\\-)*(\\d+)\\.(\\d{0," + size + "}).*$");
							/^(0+[1-9][0-9.]*)$/.test(val) && (val = val.replace(/0/g, "")),
							val = val.replace(/[。]+/g, ".").replace(/[^\d.]/g, "").replace(/\.{2,}/g, ".").replace(/^\.\.$/g, "0.").replace(/^\.$/g, "0.").replace(".", "$#$").replace(/\./g, "").replace("$#$", ".").replace(reg, "$1$2.$3")
					}
					return val;
			}
  }
}
</script>
