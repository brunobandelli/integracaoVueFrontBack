<template>
    <div >
        <h1>Painel adm!</h1>
        <br>
        <div class="columns is-centered">

        <table class="table">
            <thead >
                <tr>
                    <th>Nome</th>
                    <th>E-mail</th>
                    <th>Cargo</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td>{{user.name}}</td>
                    <td>{{user.email}}</td>
                    <td>{{user.role | processRole}}</td>
                    <td><button class="button is-success">Editar</button> | <button class="button is-danger">Deletar</button></td>
                </tr>
            </tbody>
        </table>
        </div>


            <div class="modal is-active">
                <div class="modal-background"></div>
                <div class="modal-content">
                    <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      Você quer realmente deletar o usuário?
    </p>
  </header>
  <div class="card-content">
    <div class="content">
      <p>BLA BLA BLA!</p>
    </div>
  </div>
  <footer class="card-footer">
    <a href="#" class="card-footer-item">Cancelar</a>
    <a href="#" class="card-footer-item">Sim, quero deletar!</a>
  </footer>
</div>
                </div>
            <button class="modal-close is-large" aria-label="close"></button>
            </div>

    </div>
</template>

<script>
import axios from 'axios'
export default {
    created(){

        var req = {
             headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
             }
        }
        axios.get("http://localhost:8686/user",req).then(res=>{
            console.log(res);
            this.users = res.data;
        }).catch(err =>{
            console.log(err);
        })
        console.log("OLÁ")
    },
    data()
    {
        return{
            users:[]
        }
    },
    filters: {
        processRole: function(value){
            if(value == 0){
                return "Usuário comum";
            }else if(value == 1){
                return "Admin"
            }
        }
    }
}
</script>

<style scoped>

</style>
