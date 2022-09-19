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

        this.$refs['console'][this.inputs.length-3].disabled = true;
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
                response: 'Hey! My name is Wojciech, welcome to my website.'
            },
            {
                ask: ['portfolio'],
                response: 'You can find some works here, and here'
            }
        ]

        this.inputs.push({
            id: ++this.counter,
            value: this.findResponse(expression, arr),
        });  
    },

    findResponse(expression, arr) {
        let response = '';
        let BreakException = {};
        let helpCommand = 'help';
        let helpResponse = 'List of available commands: '; 

        try {
            arr.forEach((value) => {

                if(value.ask.includes(expression.toLowerCase())) {
                    response = value.response;
                    throw BreakException
                } else if(expression.toLowerCase() == helpCommand) {
                    if(!response.includes(helpResponse)) {
                        response = helpResponse;
                    }
                    response += value.ask + ' ' + ',';
                } else {
                    response = 'Command not recognized, type help to get full list of commands.';
                }
            });
        } catch (e) {
            if (e !== BreakException) throw e;
        }

        return response;
    },
  },
}
</script>