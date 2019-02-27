<template>
    <panel-item :field="field">
        <p slot="value" class="text-90 flex">
            <span class="w-full max-col-2">
                <div
                        v-for="(label, option) in field.options"
                        :key="option"
                        class="flex-auto"
                >
                    <span
                            class="inline-block rounded-full w-2 h-2 mr-1"
                            :class="optionClass(option)"
                    />
                    <span>{{ label }}</span>
                </div>
            </span>
        </p>
    </panel-item>
</template>

<script>
    export default {
        props: ['resource', 'resourceName', 'resourceId', 'field'],

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

<style>
    .max-col-3 {
        -moz-column-count: 3;
        -webkit-column-count: 3;
        column-count: 3;
        white-space: nowrap;
    }

    .max-col-2 {
        -moz-column-count: 2;
        -webkit-column-count: 2;
        column-count: 2;
        white-space: nowrap;
    }
</style>

