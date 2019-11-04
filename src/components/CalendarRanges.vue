<template>
    <div class="ranges">
        <ul v-if="ranges">
            <li
                    v-for="(value, key) in ranges"
                    @click="$emit('clickRange', value)"
                    :data-range-key="key"
                    :key="key"
                    :class="range_class(value)"
            >{{key}}
            </li>
        </ul>
    </div>
</template>

<script>
  import moment from 'moment'

  export default {
    props: {
      ranges: Object,

      selected: Object
    },
    methods: {
      range_class (range) {
    
       const startSelect = moment(this.selected.startDate);
       const endSelect = moment(this.selected.endDate);
       const selectTime = endSelect.diff( startSelect, 'minutes');
 

        const start = moment(range[0]);
        const end = moment(range[1]);
        const rangeTime = end.diff( start, 'minutes');

        return { active: selectTime == rangeTime };

      }
    },
  }
</script>
