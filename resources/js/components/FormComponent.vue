<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card text-white bg-primary mb-3">
                
                <div class="card-header">¿En qué estás pensando ahora?</div>

                <div class="card-body">
                     

                   <form method="POST" v-on:submit.prevent="newThought()" accept-charset="utf-8">
                       <label>Ahora estoy pensando en:
                        <textarea v-model="description" name="pensamiento" class="form-control"></textarea>    
                        </label><br>
                        <button  class="btn btn-info">Enviar pensamiento</button>
                   </form>
                </div>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                description:''
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods: {
            newThought(){
                
                const params = {
                    description: this.description
                };
                this.description = '';

                axios.post('/thoughts', params)
                    .then((response) => {
                        const thought = response.data;
                        this.$emit('new', thought);
                    });
                
            }
        }
    }
</script>
