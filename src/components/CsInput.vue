<template>
	<div class="root">
	    <slot class="icon" name="icon"></slot>	
		<input 
			:value="value"
			v-on="listeners"
			:placeholder="placeholder"
			:class="{'offset': hasAddon}"
		>
		<span class="addon" :class="{'addon-split': hasAddon}">
			<slot name="addon"></slot>
		</span>
	</div>
</template>
<script>
import styles from '../assets/sass/input.scss' 
export default {
    name: 'CsInput',
    props: {
      	value: {
        	type: [String, Number],
        	description: "Input value"
      	},
      	placeholder: {
        	type: [String, Number],
			default: ""  		
      	}
    },
    computed: {
	    hasAddon() {
	        let { addon } = this.$slots;
	        return addon !== undefined;
	    },    	
      	listeners() {
        	return {
          		...this.$listeners,
          		input: this.onInput,
          		blur: this.onBlur,
          		focus: this.onFocus
        	}
      	}
    },    
    created(){

    },
	methods: {
      	onInput(evt) {
        	this.$emit('input', evt.target.value)
      	},
      	onFocus() {
        	this.focused = true;
      	},
      	onBlur() {
        	this.focused = false;
      	}
	}    
}
</script>