<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <h2><router-link to="/index">Administración de Edificios</router-link></h2>
   
        <router-link to="/create" class="btn btn-sm btn-primary">+ Departamento</router-link>
        <br>
      
  
     <router-view />
      </div>
    </div>
  </div>
</template>