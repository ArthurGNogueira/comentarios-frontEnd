export <template>
    <div v-bind:class="{ class_dark: dark }">
        <div class="container-sm">
            <div class="areaAddComent">

                <h1 class="titleAreaComent">Deixe-nos um comentário</h1>
        
                <label for="txtName">Nome: </label>
                <input v-model="nome" class="txtName form-control" type="text">

                <label for="txtmessage">messagem: </label>
                <textarea  v-model="message" class="form-control" id="txtmessageArea" cols="30" rows="10"></textarea>               

                <button v-on:click="areaAddComent" class="btnEnviar btn btn-primary btn-lg">Enviar</button>
        
                <div v-if="error == true" id="alert-message" class="alert alert-danger alert-dismissible" role="alert">
                        É necessário preencher ao menos o campo de messagem
                    <button v-on:click="error = false"  class="close" >x</button>
                </div>

            </div>
        <br>
    
        <div class="areaListComments">
            <ul class="listComments list-group">
                <li v-for="(comment, index)  in allComments" v-bind:key="comment" class="comment">
                    <h3 class="name mb-1">{{comment.nome}}</h3>
                    <p class="message mb-1">{{comment.message}}</p>

                    <button v-on:click="del(index)" class="btnExcluir btn btn-outline-danger btn-sm">Excluir</button>
                </li>
            </ul>
        </div>
    </div>
    <footer>
        <div class="custom-control custom-switch">
            <input  v-on:click="dark = !dark" type="checkbox" class="custom-control-input" id="customSwitch1">
            <label class="custom-control-label" for="customSwitch1">Dark Mode</label>
        </div>
    </footer>
    </div>
  
</template>

<script>


export default {
    data(){
        return{
            comments:[ 
                
            ],
            nome: '',
            message:'',
            error: false,
            dark: false
        };
    },
    methods:{
        areaAddComent(){
            if(this.message.trim() === ''){
                this.error = true;
            }else{
                this.comments.push({
                    nome : this.nome,
                    message : this.message,
                });

                this.nome ='',
                this.message =''
            }          
        },
        
        del(id){
            this.comments.splice(id,1);
        }
    },
    computed: {
        allComments() {
            return this.comments.map(comment => ({
                ...comment,
                nome: comment.nome.trim() == '' ? 'Anônimo' : comment.nome
            }))
        }
    },
    name: 'comentarios' 
};
</script>

<style scoped>
    .class_dark{
        background-color: rgb(45, 45, 53);
        color: white;
    }
    .class_dark .form-control{
        background-color: rgb(39, 39, 39);
        color: white;
    }
    body,
    ul,
    li,
    p{
        margin: 0px;
        padding: 0px;
        list-style: none;
        font-size: 1.2rem;
        /* font-family: Arial; */
        outline: none;
        resize: none;
    }
    a{
        text-decoration: none;
    }
    *{
        outline: none;
        border-radius: 10px;
        margin: 5px;
    }
    h1{
        font-size: 30px;
    }
    .areaAddComent, .areaListComments, footer{
        margin: 0 auto;
        width: 50%;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: flex-start;


        border: solid 1px rgb(192, 192, 192);
        padding: 20px;
        
    }
    .titleAreaComent{
        width: 100%;
    }
    .txtName{
        width: 100%; height: 30px;
    }
    #txtmessageArea{
        resize: none;
        width: 100%;
    }
    .btnEnviar, .btnExcluir{
        margin: 10px 0px;
        padding: 10px;
    }
    .close{
        outline: none;
    }
    
</style>

