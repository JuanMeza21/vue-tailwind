<script setup>
const mensaje = () => {
    console.log('Script img')
}

const borrarTargeta = (index) => {
    emit('borrarTargeta', index)
}

const editarTargeta = (index) => {
    emit('editarTargeta', index)
}

const emit = defineEmits(['borrarTargeta', 'editarTargeta'])

const props = defineProps(
    {
        name: {
            type: String,
            default: 'No name'
        },

        email: {
            type: String,
            default: 'No email'
        },

        img: {
            type: Image,
            default: 'No img'
        },

        index: {
            type: Number
        }
    }
)
</script>

<template>
    <div class="w-auto rounded shadow overflow-hidden mt-5 p-2 flex">
        <div>
            <div class="inline-block align-top" @click="mensaje">
                <img class="w-16 h-16 rounded-full" :src="props.img" alt="">
            </div>

            <div class="inline-block pl-2">
                <h2 class="text-2xl font-semibold">{{ props.name }}</h2>
                <p class="text-1x1">{{ props.email }}</p>
            </div>
        </div>

        <span @click="borrarTargeta(props.index)"
            class="w-6 h-6 grid justify-center items-center bg-red-700 text-white mt-4 ml-4 mb-4 px-3 rounded cursor-pointer hover:bg-red-800">
            X
        </span>

        <span @click="editarTargeta(props.index)"
            class="w-6 h-6 grid justify-center items-center bg-red-700 text-white mt-4 ml-2 mr-4 mb-4 px-3 rounded cursor-pointer hover:bg-red-800">
            Y
        </span>
    </div>
</template>