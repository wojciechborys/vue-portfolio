<template>
    <section>
        <article  v-for="input in inputs" :key="input.id">
            <span>> :</span><input v-on:keyup.enter="addInput" ref="console" :id="input.id" class="terminal__console--input" type="text" v-model="input.value">
        </article> 
    </section>
</template>

<script>

export default {
  name: 'AppTerminalRow',
  data() { 
    return {
        counter: 0,
        inputs: [{
            id: 0,
            value: '',
        }],
    }
  },

  methods: {
    async addInput() {
        await this.response(event.target.value);

        await this.inputs.push({
            id: ++this.counter,
            value: '',
        });

        this.$refs['console'][this.inputs.length-2].disabled = true;
        this.$refs['console'][this.inputs.length-1].focus();
    },
    
    response(expression) {
        let arr = [
            {
                ask: ['hi', 'hello', 'hey', 'how are you'],
                response: 'Hi, welcome to my site, type help for list of commands'
            }, 
            {
                ask: ['about'],
                response: 'Some info about me'
            }
        ]

        //this.findResponse(expression, arr);

        this.inputs.push({
            id: ++this.counter,
            value: this.findResponse(expression, arr),
        });  
    },

    findResponse(expression, arr) {
        let response = '';
        let BreakException = {};

        try {
            arr.forEach((value) => {

                if(value.ask.includes(expression)) {
                    response = value.response;
                    console.log(expression);
                    throw BreakException
                } else {
                    response = 'wrong';
                }
            });
        } catch (e) {
            if (e !== BreakException) throw e;
        }

        return response;
    },

   
  },

  mounted() {
    
  } 
}
</script>