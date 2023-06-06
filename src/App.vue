<script setup>
import CardComponent from './components/CardComponent.vue'
import { ref } from 'vue'

let name = ''
let email = ''
let mensajeError = ref('')

const img = 'https://www.pngall.com/wp-content/uploads/5/Profile-Male-PNG.png'

const users = ref([])

const borrarTargeta = (index) => {
  console.log('Kill to', index)

  users.value.splice(index, 1)
}

const editarTargeta = (index) => {
  let newName = prompt('Ingrese nuevo nombre: ')
  let newCorreo = prompt('Ingrese nuevo correo: ')

  if (index >= 0 && index < users.value.length) {
    users.value[index].name = newName;
    users.value[index].email = newCorreo
  }
}

const addUserr = () => {
  if (name.length > 0 && email.length > 0) {
    const newUser = {
      name: name,
      email: email,
      img: img
    }
    users.value.unshift(newUser)
    mensajeError.value = ''
  } else {
    mensajeError.value = 'Completa los campos'
  }
}

const eliminarTodo = () => {
  users.value = []
}

</script>

<template>
  <div class="flex">

    <div class="w-3/12 h-screen border-r-4">
      <div class="grid justify-center items-center relative top-[30%]">
        <h1 class="font-bold bg-[#1BCAE2] text-center">ADD PERSON</h1>
        <input class="border p-2 rounded" type="text" v-model="name" placeholder="Ingrese nombre">
        <input class="border p-2 rounded" type="text" v-model="email" placeholder="Ingrese correo">

        <button @click="addUserr" class="bg-[#1BCAE2] hover:bg-[#1BA3E2] font-bold">ADD</button>

        <div v-if="users.length > 0" class="grid justify-center items-center bg-slate-300 relative top-[20px]">
          <button @click="eliminarTodo">Eliminar todo</button>
        </div>

        <div class="m-6" v-show="mensajeError">
          <div class="flex justify-center">
            <img class="w-[60px] h-[60px]" src="https://cdn-icons-png.flaticon.com/512/1824/1824224.png" alt="">
          </div>
          <div class="">{{ mensajeError }} </div>
        </div>
      </div>
    </div>

    <div class="grid grid-cols-3 h-screen w-screen gap-2 mx-4">
      <CardComponent v-for="(user, index) in users" :key="index" :name="user.name" :email="user.email" :img="user.img"
        :index="index" @borrarTargeta="borrarTargeta" @editarTargeta="editarTargeta" />
    </div>

  </div>
</template>

<style scoped></style>