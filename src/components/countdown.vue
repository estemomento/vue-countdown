<template>
  <div class="countdown">
    <div class="day">
      <span>{{ dayToGo }}</span>
      <p>DAY{{ (dayToGo === 1) ? '' : 'S' }}</p>
    </div>
    <div class="time">
      <div class="colon first">:</div>
      <div class="hour">
        <span>{{ hourToGo.toString().padStart(2, "0") }}</span>
        <p>HOUR{{ (hourToGo === 1) ? '' : 'S' }}</p>
      </div>
      <div class="colon">:</div>
      <div class="minute">
        <span>{{ minuteToGo.toString().padStart(2, "0") }}</span>
        <p>MINUTE{{ (minuteToGo === 1) ? '' : 'S' }}</p>
      </div>
      <div class="colon">:</div>
      <div class="second">
        <span>{{ secondToGo.toString().padStart(2, "0") }}</span>
        <p>SECOND{{ (secondToGo === 1) ? '' : 'S' }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'countdown',
  props: {
    year: '',
    month: '',
    day: '',
    hour: '',
    minute: '',
    second: ''
  },
  computed: {
    timeToGo () {
      let time = Math.floor(
        (new Date(this.year, (this.month - 1), this.day, this.hour, this.minute, this.second) -
        this.now) / 1000
        )
      return (time >= 0) ? time : 0
    },
    dayToGo () {
      return Math.floor(this.timeToGo / 86400)
    },
    hourToGo () {
      return Math.floor((this.timeToGo - this.dayToGo * 86400) / 3600)
    },
    minuteToGo () {
      return Math.floor((this.timeToGo - this.dayToGo * 86400 - this.hourToGo * 3600) / 60)
    },
    secondToGo () {
      return this.timeToGo - this.dayToGo * 86400 - this.hourToGo * 3600 - this.minuteToGo * 60
    }
  },
  data: () => ({
    now: ''
  }),
  async mounted () {
    const diff = new Date((await axios.head('/')).headers.date) - new Date()
    this.now = new Date(new Date().getTime() + diff)
    window.setInterval(() => {
      this.now = new Date(new Date().getTime() + diff)
    }, 100)
  }
}
</script>

<style lang="scss" scoped>
.countdown {
  display: flex;

  @media (max-width: 767px) {
    flex-direction: column;
    align-items: center;
  }

  .time {
    display: flex;
  }

  .day, .time div {
    display: inline-flex;
    flex-direction: column;
    align-items: center;
    margin: 8px;

    @media (max-width:767px) {
      height: 60px;
      margin: 5px;
    }

    span {
      display: inline-flex;
      justify-content: center;
      align-items: center;
      width: 125px;
      height: 125px;
      font-size: 88px;
      letter-spacing: 2px;

      @media (max-width:767px) {
        width: 60px;
        height: 60px;
        font-size: 48px;
      }
    }

    p {
      font-size: 14px;
      letter-spacing: 1.58px;

      @media (max-width:767px) {
        display: none;
      }
    }
  }

  .day {
    @media (max-width:767px) {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 180px;
      width: 180px;
      border-radius: 1000px;
      border: 2px solid #fff;
      margin-bottom: 20px;

      span {
        @media (max-width:767px) {
          height: 100px;
          width: 100px;
          font-size: 88px;
        }
      }

      p {
        display: block;
      }
    }
  }

  .colon {
    height: 123px;
    width: 44px;
    font-size: 88px;
    letter-spacing: 2px;

    @media (max-width:767px) {
      height: 60px;
      width: 10px;
      font-size: 48px;
    }

    &.first {
      @media (max-width:767px) {
        display: none;
      }
    }
  }
}
</style>
