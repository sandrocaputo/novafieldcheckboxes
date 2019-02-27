<template>
    <span class="w-full">
        <span
                v-for="(value, option) in availableOptions"
                :key="option"
                :class="optionClass(option)"
                :title="value"
                class="inline-block rounded-full w-2 h-2 mr-1"
        />
    </span>
</template>

<script>
    export default {
        props: ['resourceName', 'field'],

        computed: {
            availableOptions() {
                return this.field.options
            },
        },

        methods: {

            getCheckedBoxesIds( values )
            {
                var ids = [];

                for ( var i = 0; i < values.length; i++ )
                {
                    ids.push(values[i].id);
                }

                return ids;
            },

            optionClass(option) {
                option = parseInt(option);
                var checkedIds = this.getCheckedBoxesIds( this.field.value );
                return {
                    'bg-success': this.field.value ? checkedIds.includes(option) : false,
                    'bg-danger': this.field.value ? !checkedIds.includes(option) : true,
                }
            },
        },

    }
</script>
