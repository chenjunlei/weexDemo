<template>
  <div class="warpper">
    <wxc-minibar background-color="#000">
      <image slot="left"
            src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAA1CAMAAABhhatlAAAA7VBMVEUAAAAAnvEAmvAAoPAGoPEAoPIAo/EdrPIVq/NqvfVKtfQAn/EcpPFjvPVcuvVWufQttfUAnvBnvfU7tvQ6tvQ4r/MptPUAnfBlu/RgvfVYuvVTt/RQufRGuPVDt/VCrvMApvIysvQApPEEsPMgpvH////1+//7///R6fz3/P/O6Pz4/v/9///A4vtuvvbU7PzL5/zW7vx0wPX6/v/R7P3E4/t+w/bJ5vt5wfbc8f3G5vyExfZpvPVku/RgufTZ7/2Axvfe8f2k2/qp0/h7xveFw/VmvPXp9//A5Pyu3fqt3PqlzveEyveYyfYBsPKBZcoOAAAAJXRSTlMAPj4+B0VFJBz4lRUO4cu2QA7xZ2BaNzfq1sGspYN8dVNMTBUVXAWurgAAAY9JREFUOMud1NeWgjAQgOEklLX3sr2DEekg9u728v6Pswl4OaPn7Nz+JwN8J0rQYSxH8FEKoapgUSXV7fT7jmJnc3wwML8Y8tzzkWkYxg7MqlJxROx7L2Au/vqi9iavGri5asnNPCxR6K0ajm0YA2/GoEo6Q0PUjQtG2uR9kYP5GYVqfjgQb8VnlEJWhfSLJmMGW1mRYdirBSlCm8upFU90ilsFa1j6KbXaIFZXqVUMW9G8tIoQK7WWWk0Qq7YlrbxjVjafaf+y6mVWdai60srmCfjc+sOn2BytECu2jkU29/cEnGLrQ56OxwzueuibwtoPdQb3Du+J7i1JHV5QlaKmFyL7FXcqb5iVUAp27Zb3RY8Xz3AvNafpTZkj+zXXsUW3Egafp5eWtLVcFe7kzJc3IlgqYFW1siO/D/VTGpnfGPOr8SjzK8ILrlO/4ISfj/kpNwe/HOLXGsn9p/x4wrqwX+XgRzA/66ifnvkh/4ryVzWSfjskE0349d9+GMHmYvu+b3fRrBfcR0rwYUwl5A+b5EEEIDc8lQAAAABJRU5ErkJggg=="
            style="height: 41px;width: 24px"
            ></image>
      <text style="font-size: 40px; color: #fff; font-weight:bold" slot="middle">卡尔特</text>
      <image slot="right"
            src="https://img.alicdn.com/tfs/TB1j39Uc0fJ8KJjy0FeXXXKEXXa-160-128.png"
            style="height: 32px;width: 40px"
            @click='minibarRightButtonClick'></image>
    </wxc-minibar>
      <div class="buttonBox">

        <wxc-button text='测试toast' @wxcButtonClicked="wxcButtonClicked" class="btn"></wxc-button>

        <wxc-button text='单程日历' @wxcButtonClicked="showCalendar" type='green' class="btn"></wxc-button>

        <wxc-button text='往返日历' @wxcButtonClicked="showReturnCalendar" type='yellow' class="btn"></wxc-button>

        <div class="panel">
          <text v-if="currentDate" class="text">当前日期: {{currentDate}}</text>
        </div>

        <wxc-button text='幻灯片' @wxcButtonClicked="openLightBox" type='red' class="btn"></wxc-button>

        <wxc-button text='测试Navigator跳转(体验下小游戏)' @wxcButtonClicked="goPage" type='blue' class="btn"></wxc-button>

        <wxc-button text='....' type='white' class="btn"></wxc-button>
    </div>

    <wxc-page-calendar :date-range="dateRange"
                       :animationType="animationType"
                       :selected-date="selectedDate"
                       :selected-note="selectedNote"
                       :is-range="isRange"
                       :minibar-cfg="minibarCfg"
                       :desc-list="descList"
                       @wxcPageCalendarBackClicked="wxcPageCalendarBackClicked"
                       @wxcPageCalendarDateSelected="wxcPageCalendarDateSelected"
                       ref="wxcPageCalendar">
    </wxc-page-calendar>

    <wxc-lightbox
      ref="wxc-lightbox"
      height="800"
      :show="show"
      :image-list="imageList"
      @wxcLightboxOverlayClicked="wxcLightboxOverlayClicked">
    </wxc-lightbox>
  </div>
</template>

<script>
import { WxcButton, WxcMinibar, WxcPageCalendar, WxcLightbox } from 'weex-ui'
const navigator = weex.requireModule('navigator')
const modal = weex.requireModule('modal');
export default {
  name: 'App',
  components: {
    WxcButton,
    WxcMinibar,
    WxcPageCalendar,
    WxcLightbox,
  },
  data () {
    return {
      animationType: 'push',
      currentDate: '',
      selectedDate: ['2017-06-23', '2017-06-30'],
      isRange: true,
      calendarTitle: '选择日期',
      dateRange: ['2017-06-10', '2018-06-10'],
      selectedNote: ['出发', '到达', '往返'],
      minibarCfg: {
        title: '日期选择'
      },
      descList: [
        { date: '2017-06-23', value: '￥200' },
        { date: '2017-06-24', value: '￥200' },
        { date: '2017-06-25', value: '￥200' },
        { date: '2017-06-26', value: '￥200' },
        { date: '2017-06-27', value: '￥222' },
        { date: '2017-06-28', value: '￥341' },
        { date: '2017-06-29', value: '￥230' },
        { date: '2017-06-30', value: '￥2000' }
      ],
      imageList: [
          { src: 'https://gd2.alicdn.com/bao/uploaded/i2/T14H1LFwBcXXXXXXXX_!!0-item_pic.jpg' },
          { src: 'https://gd1.alicdn.com/bao/uploaded/i1/TB1PXJCJFXXXXciXFXXXXXXXXXX_!!0-item_pic.jpg' },
          { src: 'https://gd3.alicdn.com/bao/uploaded/i3/TB1x6hYLXXXXXazXVXXXXXXXXXX_!!0-item_pic.jpg' }
      ],
      show: false,
    }
  },
  methods: {
    wxcButtonClicked() {
      modal.toast({ 'message': 'click testToastButton!', 'duration': 1 });
    },
    goPage() {
      navigator.push({
          url: 'http://192.168.1.83:8081/dist/inside.js',
          animated: "true"
        }, event => {
          modal.toast({ message: 'callback: ' + event })
        })
    },
    minibarRightButtonClick () {
      modal.toast({ 'message': 'click rightButton!', 'duration': 1 });
    },
    wxcPageCalendarDateSelected (e) {
        this.selectedDate = e.date;
        this.currentDate = e.date;
      },
    wxcPageCalendarBackClicked () {
    },
    showCalendar () {
      this.isRange = false;
      setTimeout(() => {
        this.$refs['wxcPageCalendar'].show();
      }, 10);
    },
    showReturnCalendar () {
      this.isRange = true;
      setTimeout(() => {
        this.$refs['wxcPageCalendar'].show();
      }, 10);
    },
    openLightBox () {
        this.show = true;
    },
    wxcLightboxOverlayClicked () {
    // 无状态组件，需要在此次关闭
      this.show = false;
    }
  },
}
</script>

<style scoped>
.buttonBox{
  align-items: center;
  justify-content: center;
  margin-top: 50px;
}
.btn {
  margin-bottom: 20px;
}
</style>
