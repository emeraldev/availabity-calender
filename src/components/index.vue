<template>
  <b-container>
    <b-card title="AVAILABILITY CALENDAR " sub-title="Bluegrass Digital Limited">
      <div>
        <label for="range-1">{{ jobLength }} HR/s</label>
        <b-form-input id="range-1" v-model="jobLength" @change="setLength" type="range" min="0" max="7"></b-form-input>
      </div>
      <calender :data="table" :tuples="fields"/>
    </b-card>
  </b-container>
</template>
<script>
import Calender from './calender'
import dates from '../data/dates.json'

import moment from 'moment'

export default {
  components: {
    Calender
  },
  data: () => ({
    full: [9,10,11,12,13,14,15,16,17],
    fields: [],
    job: null,
    table: [],
    jobLength: 0,
  }),
  methods: {
    checkSlotAvailability(time, jobLength, date, availabilty) {
      this.job = availabilty.find(slot => slot === time)
      if (this.job) {
        var index = this.full.indexOf(time)
        var fullTime = (index + jobLength) - 1
        var nxt = this.full[fullTime + 1]
        var buffer = availabilty.find(slot => slot === nxt)
        console.log(jobLength)
        if (buffer) {
          return 'AVAILABLE'
        } else {
          return 'UNAVAILABLE'
        }
      } else {
        return 'FULL'
      }
    },
    setLength() {
      this.table = []
      this.fields.push({
            key: '___',
          })
      var count = 0
      this.full.forEach(time => { 
        dates.forEach(date => {
          this.fields.push(
          {
            key: date.Date,
            label: moment(date.Date).format("dddd Do"),
          })
          let slot = this.checkSlotAvailability(time, this.jobLength, date.Date, date.HoursAvailable)
          var item = []
          /* item[count1] = {
            '___': count, '2016-05-18': date.Date === '2016-05-18' ? slot : '',
            '2016-05-19': date.Date === '2016-05-19' ? slot : '',
            '2016-05-20': date.Date === '2016-05-20' ? slot : '',
            '2016-05-21': date.Date === '2016-05-21' ? slot : '', 
            '2016-05-23': date.Date === '2016-05-23' ? slot : '',
            '2016-05-24': date.Date === '2016-05-24' ? slot : '',
          } */

          item = {
            '___': this.full[count + 1] ? time +':00 to ' + this.full[count + 1] + ':00' : time +':00 ', 
            '2016-05-18': '',
            '2016-05-19': '',
            '2016-05-20': '',
            '2016-05-21': '', 
            '2016-05-23': '',
            '2016-05-24': '',
          }

          if (date.Date === '2016-05-18') {
            item['2016-05-18'] = slot
            item._cellVariants = {
              '2016-05-18': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          } 
          if (date.Date === '2016-05-19') {
            item['2016-05-19'] = slot
            item._cellVariants = {
              '2016-05-19': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          } 
          if (date.Date === '2016-05-20') {
            item['2016-05-20'] = slot
            item._cellVariants = {
              '2016-05-20': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          } 
          if (date.Date === '2016-05-21') {
            item['2016-05-21'] = slot
            item._cellVariants = {
              '2016-05-21': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          } 
          if (date.Date === '2016-05-23') {
            item['2016-05-23'] = slot
            item._cellVariants = {
              '2016-05-23': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          }
          if (date.Date === '2016-05-24') {
            item['2016-05-24'] = slot
            item._cellVariants = {
              '2016-05-24': slot === 'FULL' ? 'danger' : slot === 'UNAVAILABLE' ? 'warning' : ''
            }
          }

          
          //console.log(count)

          this.table.push(item)
        });
        count++
      });
    }
  },
  mounted() {
    this.setLength()
  }
};
</script>