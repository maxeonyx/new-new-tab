<template>
    <div class=editor-panel>
        <textarea :class="valid ? '' : 'invalid'" v-model="text" v-on:focusout="format"></textarea>
        <input type="button" value="Format" @click="format" />
    </div>
</template>

<script>

const indent = 2;

export default {
    props: ['value'],
    data() {
        return {
            text: "",
        };
    },
    created() {
        this.text = localStorage.getItem('editor_text');
    },
    computed: {
        valid() {
            try {
                JSON.parse(this.text);
                return true;
            } catch {
                return false;
            }
        }
    },
    watch: {
        text() {
            localStorage.setItem('editor_text', this.text);
            try {
                let data = JSON.parse(this.text);
                this.$emit('input', data);
            } catch {
                return;
            }
        }
    },
    methods: {
        format() {
            try {
                let data = JSON.parse(this.text);
                this.text = JSON.stringify(data, null, indent);
            } catch {
                return;
            }
        },
    },
};
</script>

<style>

.editor-panel {
    position: relative;
    height: 100%;
    padding: 0;
}

.editor-panel textarea {
    width: calc(100% - 1em - 6px);
    height: calc(100% - 1em - 7px);
    padding: 0.5em;
    font-size: 1.5em;
    font-family: monospace;
    border: 3px solid rgba(0, 255.0, 0, 0.3);
    border-radius: 3px;
    resize: none;
}

.editor-panel textarea.invalid {
    border: 3px solid red;
}

.editor-panel input {
    position: absolute;
    z-index: 1;
    bottom: 3px;
    right: 3px;
}

</style>
