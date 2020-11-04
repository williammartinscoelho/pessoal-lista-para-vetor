<template>
    <div id="app">
        <div class="container">
            <div class="box-title">
                <h1>Conversor de lista para vetor</h1>
            </div>

            <div class="row">
                <div class="box-input">
                    <textarea name="list" id="list" v-model="textarea"></textarea>
                </div>

                <div class="box-output">
                    <div>

                        <div class="box-checkbox">
                            <input type="checkbox" id="ordem_alfabetica" v-model="check_ordem_alfebetica">
                            <label for="ordem_alfabetica">Ordem Alfabética</label>
                        </div>
                        
                        <div class="box-checkbox">
                            <input type="checkbox" id="remover_vazios" v-model="check_remover_vazio">
                            <label for="remover_vazios">Remover espaços vazios</label>
                        </div>

                        <div class="box-checkbox">
                            <input type="checkbox" id="remover_espacos" v-model="check_remover_espacos">
                            <label for="remover_espacos">Remover espaços no final das palavras</label>
                        </div>
                        
                    </div>

                    <p ref="vetor">{{vetor}}</p>

                    <textarea name="vetor" id="vetor" ref="vetor">{{vetor}}</textarea>

                    <button v-on:click="copy">Copiar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'App',
        data: function() {
            return {
                textarea: "input here",
                check_ordem_alfebetica: false,
                check_remover_vazio: false,
                check_remover_espacos: true
            }
        },
        computed: {
            vetor: function() {
                
                let text = this.textarea;
                text = text.split('\n');
                
                if (this.check_ordem_alfebetica) {
                    text.sort();
                }

                if (this.check_remover_espacos) {
                    for (let i = 0; i < text.length; i++) {
                        text[i] = text[i].trim();
                    }
                }

                if (this.check_remover_vazio) {
                    text = text.filter( e => e !== "");
                }
                
                return text;
            }
        },
        methods: {
            copy: function() {
                this.$refs.vetor.select();
                document.execCommand("copy");
                alert("copied to clipboard");
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .container {
        margin: 0 50px ;
    }

    .box-title {
        text-align: center;
    }

    .row {
        display: flex;
        padding-top: 15px;
    }

    .box-input {
        flex: 1;
    }

    .box-input textarea {
        width: 90%;
        height: 90vh;
        padding: 5px;
    }

    .box-output {
        flex: 1;
    }

    .box-output .box-checkbox {
        margin-bottom: 15px;
    }

    .box-output input {
        margin-right: 15px;
    }

    .box-output p {
        margin-bottom: 15px;
    }

    .box-output textarea {
        width: 0px;
        height: 0px;
        border-color: white;
        margin-right: 1px;
    }

    .box-output button {
        padding: 10px;
        cursor: pointer;
    }
</style>
