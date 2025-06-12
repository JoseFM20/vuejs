<template>
    <!--PAGINATION -->
    <div class="pt-2 text-center">
        <span>Showing {{ paginationData.from }} to {{ paginationData.total }} results</span>
        <Bootstrap5Pagination :date="paginationData" @pagination-change-page="paginationChange" class="pt-4" :limit=0
            align="center" :keepLength="true" :show-disabled="true">
        </Bootstrap5Pagination>
    </div>
</template>

<script setup>
import { Bootstrap5Pagination } from 'laravel-vue-pagination';
// props nos ayuda a recibir la información del componente padre
const props = defineProps({
    paginationData: {
        type: Object,
        required: true
    }
})
// Emit nos ayuda a regresar el valor seleccionado al componente padre
const emit = defineEmits(['paginationChange'])

const paginationChange = (page) => {
    emit('paginationChange', page)
}
</script>