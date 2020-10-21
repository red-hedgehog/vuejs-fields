<template>
    <label class="is-centered">
        <div class="is-text  margin-top-20 is-bold">{{ label }}</div>
        <input
            class="is-text"
            :class="{ invalid: isInvalid }"
            :type="type"
            :value="value"
            :required="required"
            :maxlength="maxlength"
            v-on="$listeners"
            @blur="validate"
            @input="$emit('update', $event.target.value)"
        />
    </label>
</template>

<script>
export default {
    model: {
        prop: 'value',
        event: 'update',
    },
    props: {
        value: {
            type: String,
            default: null,
        },
        label: {
            type: String,
            default: '',
        },
        type: {
            type: String,
            default: 'text',
        },
        required: {
            type: Boolean,
            default: false,
        },
        maxlength: {
            type: Number,
            default: null,
        },
        validator: {
            type: Function,
            default: null,
        },
    },
    data() {
        return {
            isInvalid: null,
        };
    },
    methods: {
        validate() {
            if (!this.validator) {
                this.isInvalid = false;
                return;
            }
            this.isInvalid = !this.validator();
        },
    },
};
</script>
