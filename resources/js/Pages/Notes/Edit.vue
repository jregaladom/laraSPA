
<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Módulo de Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">  
                <div class="md:grid md:grid-cols-3 md:gap-6">
                    <div class="md:col-span-1">
                        <div class="px-4 sm:px0">
                            <h3 class="text-lg text-gray-900">Editar nota</h3>
                            <p class="text-sm text-gray-600">Si editas no podrás volver al estado anterior</p>
                        </div>
                    </div>
                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded-md p-4">
                        <form @submit.prevent="submit"> 
                            <label class="block font-medium text-sm text-gray-700">Resumen</label>
                            <textarea name="" id="" cols="30" rows="10" class="form-input w-full rounded-md shadow-sm" v-model="form.excerpt">
                            </textarea>

                            <label class="block font-medium text-sm text-gray-700">Contenido</label>
                            <textarea name="" id="" cols="30" rows="10" class="form-input w-full rounded-md shadow-sm" v-model="form.content" :rows="8">
                            </textarea>
                            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">Editar</button>
                            
                        </form>
                        <hr class="my-6">
                        <a class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-md" href="" @click.prevent="destroy">
                        Eliminar nota
                        </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Link } from '@inertiajs/vue3'

export default {
    components: {
        AppLayout,
        Link
    },
    props:{
        note: Object
    },
    data(){
        return {
            form: {
                content: this.note.content,
                excerpt: this.note.excerpt,
            }
        }
    },
    methods: {
        submit(){
            this.$inertia.put(route('notes.update', this.note.id), this.form)
        },
        destroy(){
            if(confirm('¿Estás seguro de eliminar la nota?')){
                this.$inertia.delete(route('notes.destroy', this.note.id))
            }
            
        }
    }
}
</script>

