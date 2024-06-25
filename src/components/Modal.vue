<template>
    <Teleport to="body">
        <div v-if="show" class="backdrop" @click="toggleBackdropHandler"></div>
        <dialog :open="show" class=" z-[999] rounded-xl p-6  overflow-hidden">
            <div>
                <header class="p-3">
                    <slot name="modal-header">

                    </slot>
                </header>
                <main class="p-3">
                    <slot name="modal-content">

                    </slot>
                </main>
                <!-- Action -->
                <div class="flex gap-3 justify-end">
                    <slot />
                </div>

            </div>
        </dialog>
    </Teleport>
</template>

<script setup>
const props = defineProps(['show'])
const emit = defineEmits(['toggleBackdrop'])

const toggleBackdropHandler = () => {
    emit('toggleBackdrop', props.show)
    console.log(props.show);
}


</script>

<style scoped>
.backdrop {
    position: fixed;
    /* Ensures the backdrop covers the entire viewport */
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    /* Semi-transparent black */
    z-index: 99;
    /* Ensure it's on top of other content */
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    position: fixed;
    inset: 0px;
    margin: 0px;
    display: grid;
    height: 100%;
    max-height: none;
    width: 100%;
}
</style>