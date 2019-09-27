<template>
    <section>
        <p class="content"><b>Selected:</b> {{ selected }}</p>
        <b-field label="Find a name">
            <b-autocomplete
                v-model="name"
                placeholder="e.g. Anne"
                :keep-first="keepFirst"
                :open-on-focus="openOnFocus"
                :data="filteredDataObj"
                field="user.first_name"
                @select="option => selected = option">
                <template slot="middle" slot-scope="props">
                   <a
                            v-for="(option, index) in data"
                            :key="index"
                            class="dropdown-item"
                            :class="{ 'is-hovered': option === hovered }"
                            @click="setSelected(option)">

                            <slot
                                v-if="hasDefaultSlot"
                                :option="option"
                                :index="index"
                            />
                            <span v-else>
                                {{ getValue(option, true) }}
                            </span>
                        </a>
                </template>
            </b-autocomplete>
        </b-field>
    </section>
</template>

<script>
    const data = require('@/data/sample.json')

    export default {
        data() {
            return {
                data,
                keepFirst: false,
                openOnFocus: false,
                name: '',
                selected: null
            }
        },
        computed: {
            filteredDataObj() {
                return this.data.filter((option) => {
                    return option.user.first_name
                        .toString()
                        .toLowerCase()
                        .indexOf(this.name.toLowerCase()) >= 0
                })
            }
        }
    }
</script>
