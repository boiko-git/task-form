<template>
    <div 
        class="custom-input"
        :class="{'custom-input_error': error}" 
    >
        <input 
            class="custom-input__input"
            ref="input" 
            :readonly="readonly" 
            :id="elId || false" 
            :autofocus="autofocus" 
            :type="type || 'text'" 
            :placeholder="placeholder || ''" 
            @input="$emit('oninput', $event.target.value)" 
            :value="value" 
            @focus="$emit('onfocus')" 
            @blur="$emit('onblur')"
        >
        <span class="custom-input__error">error</span>
    </div>
</template>

<script>
export default {
    props: ['value', 'error', 'errorText', 'type', 'placeholder', 'autofocus', 'el-id', 'readonly'],
    methods: {
        blur() {
            this.$refs.input.blur()
        },
        focus() {
            this.$refs.input.focus()
        }
    }
}
</script>

<style lang="scss" scoped>
.custom-input {
    position: relative;
    width: 100%;
 
    &__input {
        width: 100%;
        height: 60px;
        background: rgba(167, 217, 234, 0.24);  
        border-radius: 10px;
        border: 1px solid rgba(167, 217, 234, 0.24);
        outline: none;
        padding: 0 20px;
        font-weight: 300;
        font-size: 17px;
        letter-spacing: 0.01em;
        color: #005A71;
        -webkit-appearance: none;
        transition: border-color .35s ease;

        &::placeholder {
            color: #b3b3b3;
        }

        &:focus {
            border-color: rgba(167, 217, 234, 1);
        }
    }

    &__error {
        position: absolute;
        bottom: calc(100% + 12px);
        right: 0;
        font-weight: 300;
        font-size: 15px;
        line-height: 20px;
        text-align: right;
        letter-spacing: 0.01em;
        color: #FF4633;
        opacity: 0;
        transition: opacity .5s ease;
        pointer-events: none;
    }

    &_error {
        .custom-input__input{
            color: #FF4633;
            border-color: #FF4633;
        }

        .custom-input__error {
            opacity: 1;
            pointer-events: all;
        }
    }
}
</style>
    