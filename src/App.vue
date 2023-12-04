<script setup>
import { useFullscreen } from "@vueuse/core";
import autofit from "autofit.js";
import videojs from "video.js";
import "video.js/dist/video-js.css";
import { onMounted, reactive, ref } from "vue";
import bgPoster from "./assets/img.png";
import btn from "./assets/微信图片_20231202205845.png";
import message from "./assets/机场信息.png";
import bgVideo from "./assets/WeChat_one.mp4";
import bridImg from './assets/brid.png'

const videoPlayer = ref(null);
const myPlayer = ref(null);
const myPlayer1 = ref(null);

const { isFullscreen, enter, exit, toggle } = useFullscreen();
const isClick = ref(false);
const isClick2 = ref(false);
const isClick3 = ref(false);
const areX = ref(1);
const visible = ref(false);
const visible2 = ref(false);
const visible3 = ref(false);
const TabStyle = {
  backgroundImage: "linear-gradient(to right , #7A88FF, #7AFFAF)",
  // 透明度
};
const TabStyle1 = {
  backgroundImage: "linear-gradient(to right , #7A88FF, #7AFFAF)",
  // 透明度
  position:'relative',
  left:"13.5%",
  opacity: 1,
};
const maskStyle = {
  opacity: 0,
};

const columns = [
  { title: "基本参数", dataIndex: "title1" },
  { title: "跑道全长(米)", dataIndex: "title2" },
  { title: "设计等级", dataIndex: "title3" },
  { title: "目前使用等级", dataIndex: "title4", width: 120 },
  { title: "跑道宽度", dataIndex: "title5" },
  { title: "跑道道肩", dataIndex: "title6" },
  { title: "主滑行道(条)", dataIndex: "title7" },
  { title: "主滑行道尺寸", dataIndex: "title8" },
  { title: "快速脱离滑行道", dataIndex: "title9" },
  { title: "启用时间", dataIndex: "title10" },
];
const data = reactive([
  {
    title1: "17L-35R一跑道",
    title2: "4000",
    title3: "双向CATI/MI4E",
    title4: "双向CATI 4E",
    title5: "60",
    title6: "1.5",
    title7: "2",
    title8: "4000x29",
    title9: "6",
    title10: "1999",
  },
]);
onMounted(() => {
  autofit.init({
    designHeight: 1440,
    designWidth: 2560,
    renderDom: "#app",
    resize: true,
  });

  // 为myPlayer元素赋值，使用videojs函数创建视频播放器
  myPlayer.value = videojs(
    videoPlayer.value,
    {
      // 播放器自动播放设置为false
      autoplay: false,
      // 播放器显示的封面图片
      poster: bgPoster,
      // 播放器显示控制条
      controls: false,
      // 播放器开始静音
      muted: true,
      // 播放器的视频源
      sources: [
        {
          // 视频源的URL
          src: bgVideo,
          // 视频源的类型
          type: "video/mp4",
        },
      ],
      // 播放器的控制栏
      controlBar: false,
      // 播放器的用户操作
      userActions: false,
    },
    () => {
      // 播放器加载完成时执行的回调函数
      myPlayer.value.log("play.....");
    }
  );
  myPlayer.value.on("playing",function(){
    visible2.value=true;
  })
  // 监听播放器播放结束事件
  myPlayer.value.on("ended", function () {
    // 打印日志信息
    console.log("eee");
    // 将isClick的值设为false
    isClick.value = false;
    isClick2.value = true;
    areX.value = 2;
    visible2.value=false
  });
});





const throttle = (fn, wait = 50) => {
  // 上一次执行 fn 的时间
  let previous = 0;
  // 将 throttle 处理结果当作函数返回
  return function (...args) {
    // 获取当前时间，转换成时间戳，单位毫秒
    let now = +new Date();
    // 将当前时间和上一次执行函数的时间进行对比
    // 大于等待时间就把 previous 设置为当前时间并执行函数 fn
    if (now - previous > wait) {
      previous = now;
      fn.apply(this, args);
    } else {
      areX.value = 2;
    }
  };
};

// DEMO
// 执行 throttle 函数返回新函数
// const betterFn = throttle(() => {
//   isClick.value = true;
//   myPlayer.value.currentTime(0);
//   myPlayer.value.play();
// }, 27000);
// // 每 10 毫秒执行一次 betterFn 函数，但是只有时间差大于 1000 时才会执行 fn

const bgClick = () => {
  isClick.value = true;
  myPlayer.value.currentTime(0);
  myPlayer.value.play();
  isClick2.value=false;

};
const menuClick = (x) => {

  switch (x) {
    case 1:
      data.splice(0);
      data.push({
        title1: "17L-35R一跑道",
        title2: "4000",
        title3: "双向CATI/MI4E",
        title4: "双向CATI 4E",
        title5: "60",
        title6: "1.5",
        title7: "2",
        title8: "4000x29",
        title9: "6",
        title10: "1999",
      });
      visible.value = true;
      break;
    case 2:
      data.splice(0);
      data.push({
        title1: "16R-35L二跑道",
        title2: "3800",
        title3: "双向CATI/MI4E",
        title4: "16R CATI 4F 34L CATII/IIA 4F",
        title5: "60",
        title6: "7.5",
        title7: "2",
        title8: "3800x25",
        title9: "4",
        title10: "2005",
      });
      visible.value = true;
      break;
    case 3:
      data.splice(0);
      data.push({
        title1: "17R-35L三跑道",
        title2: "3400",
        title3: "双向CATI 4F",
        title4: "双向CATI 4F",
        title5: "60",
        title6: "7.5",
        title7: "2",
        title8: "3400x25",
        title9: "12",
        title10: "2008",
      });
      visible.value = true;
      break;
    case 4:
      data.splice(0);
      data.push({
        title1: "16L-34R四跑道",
        title2: "3800",
        title3: "双向CAT II/M4F",
        title4: "双向CATI 4F",
        title5: "60",
        title6: "7.5",
        title7: "2",
        title8: "3800x25",
        title9: "12",
        title10: "2015",
      });
      visible.value = true;
      break;
      case 5:
        visible3.value = true;
        break;
        case 6:

          myPlayer.value.currentTime(0);
          myPlayer.value.pause()
          // 将第图层重新切换为第一个图层
          isClick2.value = false;
          isClick.value = false;
          isClick3.value = true;
          break;
    default:
      break;
  }
};
const handleCancel = () => {
  visible.value = false;
};
const handleOk = () => {
  visible.value = false;
};
const videoClick = () => {
  // 清除videojs函数创建的视频播放器
  myPlayer.value.currentTime(0);
myPlayer.value.pause()
  // 将第图层重新切换为第一个图层
  isClick2.value = false;
  isClick.value = false;
  isClick3.value = true;

};
</script>

<template>
  <!--@click="bgClick"-->


  <div class="con ">


    <div style="color: #f6f3f3;right: 1%;top:1%;opacity: 0.7" class="absolute z-9999 "><icon-close-circle-fill style="width: 50px;height: 50px" @click=""/></div>
<!--<div><img alt="" class="absolute z-9999" :src="backImg" width="540" height="140" style="top: 10%; left: 50.5%;"/>-->
<!--  <span class="absolute z-9999" style="top: 10%; left: 50.5%;color: white"><h1>浦东机场飞行区信息展示屏</h1></span>-->
<!--</div>-->

    <div :class="!isClick ? 'absolute z-999 !w-full !h-full' : 'absolute !w-full !h-full'">
      <img alt=""

        @click.prevent="bgClick"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 75%; left: 47%"
      />
      <!-- <img alt="" class="absolute z-999" :src="btn" width="140" height="140"/>
      <img alt="" class="absolute z-999" :src="btn" width="140" height="140"/>
      <img alt="" class="absolute z-999" :src="btn" width="140" height="140"/>
      <img alt="" class="absolute z-999" :src="btn" width="140" height="140"/> -->
      <img alt=""

        @click.stop="menuClick(1)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 72%; left: 25%"
      />
      <img alt=""
        @click.stop="menuClick(2)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 16%; left: 30%"
      />
      <img alt=""
        @click.stop="menuClick(3)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 84%; left: 25%"
      />
      <img alt=""
        @click.stop="menuClick(4)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 5%; left: 30%"
      />
      <img alt=""
        :src="bgPoster"
        class="!w-full !h-full !max-w-full !max-h-full !min-h-full !min-w-full"
      />
      <img alt=""
          @click.stop="menuClick(5)"
          class="absolute anima"
          :src="btn"
          width="60"
          height="60"
          style="top: 87%; left: 2%"
      />
      <div style="top: 77%; left: 25.5%;font-size: 20px;color: #ffffff;" :class="isClick ? ' absolute z-999 ' : 'absolute '">跑道①</div>
      <div style="top: 21%; left: 30.5%;font-size: 20px;color: #ffffff;" :class="isClick ? ' absolute z-999 ' : 'absolute '">跑道②</div>
      <div style="top: 89%; left: 25.5%;font-size: 20px;color: #ffffff;" :class="isClick ? ' absolute z-999 ' : 'absolute '">跑道③</div>
      <div style="top: 10%; left: 30.5%;font-size: 20px;color: #ffffff;" :class="isClick ? ' absolute z-999 ' : 'absolute '">跑道④</div>
      <div style="top: 80%; left: 46.8%;font-size: 20px;color: #ffffff;" :class="isClick ? ' absolute z-999 ' : 'absolute '">机场信息</div>
      <div style="top: 85%; left: 2%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">鸟情监测</div>

<!--      <img alt=""-->
<!--          @click.stop="menuClick(6)"-->
<!--          class="absolute anima"-->
<!--          :src="btn"-->
<!--          width="60"-->
<!--          height="60"-->
<!--          style="top: 93%; left: 94%"-->
<!--      />-->
    </div>
    <video
      ref="videoPlayer"
      :class="
        isClick
          ? 'absolute z-999 video-js !min-h-full !min-w-full !max-w-full !max-h-full !w-full !h-full !object-cover'
          : 'absolute video-js !min-h-full !min-w-full !max-w-full !max-h-full !w-full !h-full !object-cover'
      "
      @click="videoClick"
      webkit-playsinline="webkit-playsinline"
      playsinline="playsinline"
    ></video>
    <a-modal
      :visible="visible"
      @ok="handleOk"
      :closable="false"
      :mask-style="maskStyle"
      @cancel="handleCancel"
      width="50%"
      :modal-style="TabStyle"
      :footer="false"
    >
      <a-table
        :pagination="false"
        :columns="columns"
        :data="data"
        :style="TabStyle"
      ></a-table>
    </a-modal>
    <a-modal
        v-model:visible="visible2"
        @ok="handleOk"
        :closable="false"
        @cancel="handleCancel"
        :mask-style="maskStyle"
        :modal-style="TabStyle1"
        :footer="false"
        :hide-title="true"
        :align-center="false"

        top="30%"
        :width="470"
    >
      <div style="text-align: center">
        <h1>机场总面积20.2平方千米</h1>
        <a-image :src="message" width="100%" height="100%"></a-image>
      </div>
    </a-modal>
    <a-modal
        v-model:visible="visible3"
        @ok="handleOk"
        :closable="false"
        @cancel="handleCancel"
        :mask-style="maskStyle"
        :modal-style="TabStyle"
        :footer="false"
        :hide-title="true"
        :width="700"
    >
      <div>
        <a-image :src="bridImg" width="100%" height="100%"></a-image>

      </div>
    </a-modal>
    <div :class="isClick2 ? ' absolute z-999 threePage' : 'absolute threePage'">
      <img alt=""
        @click="menuClick(1)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 72%; left: 25.3%"
      />
      <div style="top: 77%; left: 25.5%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">跑道①</div>
      <div style="top: 10%; left: 30.5%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">跑道④</div>
      <div style="top: 89%; left: 25.5%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">跑道③</div>
      <div style="top: 21%; left: 30.5%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">跑道②</div>
      <div style="top: 80%; left: 46.8%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">机场信息</div>

      <div style="top: 85%; left: 2%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">鸟情监测</div>
      <img alt=""

           @click.prevent="bgClick"
           class="absolute anima"
           :src="btn"
           width="60"
           height="60"
           style="top: 75%; left: 44%"
      />
      <img alt=""
        @click.stop="menuClick(2)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 16%; left: 24%"
      />
      <img alt=""
        @click.stop="menuClick(3)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 84%; left: 16%"
      />
      <img alt=""
        @click.stop="menuClick(4)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style=" top: 5%; left: 18%"
      />
      <img alt=""
          @click.stop="menuClick(5)"
          class="absolute anima"
          :src="btn"
          width="60"
          height="60"
          style="top: 87%; left:-13.5%"
      />
      <img alt=""
          @click.stop="menuClick(6)"
          class="absolute anima"
          :src="btn"
          width="60"
          height="60"
          style="top: 93%; left: 77%"
      />
      <div style="top: 90.5%; left: 96.3%;font-size: 20px;color: #ffffff;" :class="isClick2 ? ' absolute z-999 ' : 'absolute '">重置</div>
      <a-modal
        :visible="visible"
        @ok="handleOk"
        :closable="false"
        @cancel="handleCancel"
        :mask-style="maskStyle"
        width="50%"
        :modal-style="TabStyle"
        :footer="false"
      >
        <a-table
          :pagination="false"
          :columns="columns"
          :data="data"
          :style="TabStyle"
        ></a-table>
      </a-modal>
    </div>
    <div :class="isClick3 ? ' absolute z-999 bgPoster' : 'absolute bgPoster'">


    </div>
  </div>
</template>

<style>
* {
  -moz-user-select: none; /* Firefox */
  -webkit-user-select: none; /* Safari/Webkit */
  -ms-user-select: none; /* IE10+ */
  user-select: none;
}
.con {
  position: relative;
  width: 100% !important;
  height: 100% !important;
  overflow: hidden;
}

.vjs-poster img  {
  width: 100% !important;
  height: 100% !important;
  //object-fit: fill !important;
}

.threePage {
  background-image: url(./assets/one.png);
  position: fixed;
  width: 100%;
  height: 100%;
  background-size: 100% 100%;
}
.threePage img  {
  position: relative;
}
.anima {
  animation-name: likes;
  animation-direction: alternate;
  animation-timing-function: linear;
  animation-delay: 0s;
  animation-iteration-count: infinite;
  animation-duration: 1s;
}

@keyframes likes {
  0% {
    transform: scale(1);
  }
  25% {
    transform: scale(0.9);
  }
  50% {
    transform: scale(0.85);
  }
  75% {
    transform: scale(0.9);
  }
  100% {
    transform: scale(1);
  }
}

</style>
