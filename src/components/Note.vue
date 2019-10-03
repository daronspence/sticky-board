<template>
    <div ref="note" class="note bg-yellow-200 w-32 h-32 p-4 relative border flex items-stretch shadow-lg">
        <moveable v-bind="moveable" @drag="handleDrag" class="absolute top-0 left-0 cursor-move">
            <span class="focus:outline-none text-gray-900 block">
                <svg viewBox="0 0 20 20" class="fill-current w-2 h-2" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                    <g id="Page-1" stroke="none" stroke-width="1" fill-rule="evenodd">
                        <g id="icon-shape">
                            <path d="M0,8.00585866 C0,6.89805351 0.897060126,6 2.00585866,6 L11.9941413,6 C13.1019465,6 14,6.89706013 14,8.00585866 L14,17.9941413 C14,19.1019465 13.1029399,20 11.9941413,20 L2.00585866,20 C0.898053512,20 0,19.1029399 0,17.9941413 L0,8.00585866 L0,8.00585866 Z M6,8 L2,8 L2,18 L12,18 L12,14 L15,14 L15,12 L18,12 L18,2 L8,2 L8,5 L6,5 L6,8 L12,8 L12,14 L17.9941413,14 C19.1029399,14 20,13.1019465 20,11.9941413 L20,2.00585866 C20,0.897060126 19.1019465,0 17.9941413,0 L8.00585866,0 C6.89706013,0 6,0.898053512 6,2.00585866 L6,8 Z" id="Combined-Shape"></path>
                        </g>
                    </g>
                </svg>
            </span>
        </moveable>
        <button @click="remove" class="absolute top-0 right-0 text-xs font-serif text-gray-900">
            <svg viewBox="0 0 20 20" class="fill-current w-2 h-2" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <g id="Page-1" stroke="none" stroke-width="1" fill-rule="evenodd">
                    <g id="icon-shape">
                        <polygon id="Combined-Shape" points="10 8.58578644 2.92893219 1.51471863 1.51471863 2.92893219 8.58578644 10 1.51471863 17.0710678 2.92893219 18.4852814 10 11.4142136 17.0710678 18.4852814 18.4852814 17.0710678 11.4142136 10 18.4852814 2.92893219 17.0710678 1.51471863 10 8.58578644"></polygon>
                    </g>
                </g>
            </svg>
        </button>
        <textarea class="w-full bg-transparent resize-none text-xs" v-model="body"></textarea>
    </div>
</template>

<script>
import Moveable from 'vue-moveable'

export default {
    props: ['note'],
    components: {
        Moveable,
    },
    data() {
        return {
            xpos: 0,
            ypos: 0,
            body: '',
            moveable: {
                draggable: true,
                throttleDrag: 0,
            },
        }
    },
    mounted() {
        const note = this.note

        this.xpos = note.xpos || note.id * 1 
        this.ypos = note.ypos || note.id * 1

        this.body = note.body

        this.$refs.note.style.top = this.ypos + '%';
        this.$refs.note.style.left = this.xpos + '%';
    },
    methods: {
        handleDrag({ clientX, clientY }) {
            // console.log('onDrag left, top', clientX, clientY);
            const windowWidth = window.innerWidth;
            const windowHeight = window.innerHeight;

            // console.log(windowWidth, windowHeight)
            const top = clientY / windowHeight * 100;
            const left = clientX / windowWidth * 100;

            this.$refs.note.style.left = `${left}%`;
            this.$refs.note.style.top = `${top}%`;
        },
        remove() {
            this.$refs.note.style.display = 'none';
        }
    }
}
</script>

<style>
.note {
    position: absolute;
    font-family: fantasy;
}
</style>