<template>
  <div class="warpper">
    <wxc-minibar background-color="#000">
      <image slot="left"
            src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAA1CAMAAABhhatlAAAA7VBMVEUAAAAAnvEAmvAAoPAGoPEAoPIAo/EdrPIVq/NqvfVKtfQAn/EcpPFjvPVcuvVWufQttfUAnvBnvfU7tvQ6tvQ4r/MptPUAnfBlu/RgvfVYuvVTt/RQufRGuPVDt/VCrvMApvIysvQApPEEsPMgpvH////1+//7///R6fz3/P/O6Pz4/v/9///A4vtuvvbU7PzL5/zW7vx0wPX6/v/R7P3E4/t+w/bJ5vt5wfbc8f3G5vyExfZpvPVku/RgufTZ7/2Axvfe8f2k2/qp0/h7xveFw/VmvPXp9//A5Pyu3fqt3PqlzveEyveYyfYBsPKBZcoOAAAAJXRSTlMAPj4+B0VFJBz4lRUO4cu2QA7xZ2BaNzfq1sGspYN8dVNMTBUVXAWurgAAAY9JREFUOMud1NeWgjAQgOEklLX3sr2DEekg9u728v6Pswl4OaPn7Nz+JwN8J0rQYSxH8FEKoapgUSXV7fT7jmJnc3wwML8Y8tzzkWkYxg7MqlJxROx7L2Au/vqi9iavGri5asnNPCxR6K0ajm0YA2/GoEo6Q0PUjQtG2uR9kYP5GYVqfjgQb8VnlEJWhfSLJmMGW1mRYdirBSlCm8upFU90ilsFa1j6KbXaIFZXqVUMW9G8tIoQK7WWWk0Qq7YlrbxjVjafaf+y6mVWdai60srmCfjc+sOn2BytECu2jkU29/cEnGLrQ56OxwzueuibwtoPdQb3Du+J7i1JHV5QlaKmFyL7FXcqb5iVUAp27Zb3RY8Xz3AvNafpTZkj+zXXsUW3Egafp5eWtLVcFe7kzJc3IlgqYFW1siO/D/VTGpnfGPOr8SjzK8ILrlO/4ISfj/kpNwe/HOLXGsn9p/x4wrqwX+XgRzA/66ifnvkh/4ryVzWSfjskE0349d9+GMHmYvu+b3fRrBfcR0rwYUwl5A+b5EEEIDc8lQAAAABJRU5ErkJggg=="
            style="height: 41px;width: 24px"></image>
      <text style="font-size: 40px; color: #fff; font-weight:bold" slot="middle">卡尔特-内页</text>
    </wxc-minibar>
    <wxc-lottery-rain :config="config"
                    :pic-list="images"
                    ref="wxc-lottery-rain"
                    :wrap-style="wrapStyle"
                    class="rainBox"
                    @wxcLotteryRainCaught="wxcLotteryRainCaught">
    </wxc-lottery-rain>
  </div>
</template>

<script>
import { WxcMinibar, WxcLotteryRain  } from 'weex-ui'
const modal = weex.requireModule('modal');
export default {
  name: 'App',
  components: {
    WxcMinibar,
    WxcLotteryRain,
    },
  data: () => ({
      images: [
       'https://img.alicdn.com/tfs/TB1sZPlb5IRMeJjy0FbXXbnqXXa-241-206.png',
       'https://img.alicdn.com/tfs/TB1eCbwb3MPMeJjy1XcXXXpppXa-241-206.png',
       'https://img.alicdn.com/tfs/TB1rDTjb3MPMeJjy1XdXXasrXXa-241-206.png',
       'https://img.alicdn.com/tfs/TB1Nw2sb3MPMeJjy1XbXXcwxVXa-241-206.png',
       'https://img.alicdn.com/tfs/TB1hCbwb3MPMeJjy1XcXXXpppXa-241-206.png'
      ],
      config: {
        intervalTime: 450,
        hideAniTime: 300,
        showAniTime: 300,
        showTime: 450,
        randomTime: 300,
        width: 241,
        height: 206
      },
      wrapStyle: {
        backgroundColor: 'rgba(133, 11, 11, .7)'
      }
    }),
  methods: {
      wxcLotteryRainCaught (e) {
        modal.toast({ 'message': `点中啦！ID：${e.rainId}`, 'duration': 1 });
      }
    }
}
</script>

<style scoped>
    .rainBox{
        margin-top: 90px;
    }
</style>
