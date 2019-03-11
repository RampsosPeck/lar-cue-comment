<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card bg-info mb-3">
                    
                    <div class="card-header">Publicado en {{ thought.created_at }}</div>

                    <div class="card-body">
                        <input v-if="editMode" type="text" class="form-control" v-model="thought.description">
                        <p v-else >{{ thought.description }}</p>
                    </div>
                    <div class="card-footer">
                        <button v-if="editMode" v-on:click="onClickUpdate()" class="btn btn-warning">Guardar Cambios</button>
                        <button v-else v-on:click="onClickEdit()" class="btn btn-warning">Editar</button>
                        <button v-on:click="onClickDelete()" class="btn btn-danger">Eliminar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['thought'],
        data() {
            return{
                editMode: false 
            } 
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods: {
            onClickDelete(){
                axios.delete('/thoughts/${this.thought.id}').then(() => {
                    this.$emit('delete');
                });    

            },
            onClickEdit(){

                this.editMode = true;
            },
            onClickUpdate(){
                const params = {
                    description: this.thought.description
                };
                axios.put('/thoughts/${this.thought.id}', params).then((response)=>{
                    this.editMode = false;
                    const thought  = response.data;
                    this.$emit('update', thought);
                });

            }
        }
    }
</script>
