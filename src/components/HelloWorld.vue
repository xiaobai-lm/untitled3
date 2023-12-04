<script setup>
import { useFullscreen } from "@vueuse/core";
import autofit from "autofit.js";
import videojs from "video.js";
import "video.js/dist/video-js.css";
import { onMounted, onUnmounted, reactive, ref } from "vue";
import bgPoster from "./assets/img.png";
import btn from "./assets/微信图片_20231202205845.png";
import message from "./assets/机场信息.jpg";
import bgVideo from "./assets/WeChat_20231204050304.mp4";

const videoPlayer = ref(null);
const myPlayer = ref(null);
const { isFullscreen, enter, exit, toggle } = useFullscreen();
const isClick = ref(false);
const isClick2 = ref(false);
const isClick3 = ref(false);
const areX = ref(1);
const visible = ref(false);
const visible2 = ref(false);
const TabStyle = {
  backgroundImage: "linear-gradient(to right , #7A88FF, #7AFFAF)",
  // 透明度
};
const TabStyle1 = {
  backgroundImage: "linear-gradient(to right , #7A88FF, #7AFFAF)",
  // 透明度
  opacity: 0.9,
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
    // isClick.value = false;
    // isClick2.value = true;
  })
  // 监听播放器播放结束事件
  myPlayer.value.on("ended", function () {
    // 打印日志信息
    console.log("eee");
    // 将isClick的值设为false
    isClick.value = false;
    isClick2.value = true;
    myPlayer.value.dispose;
  });
});

onUnmounted(() => {
  if (myPlayer.value) {
    myPlayer.value.dispose();
  }
});

const bgDbClick = () => {
  enter();
};

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
    

    }
  };
};

// DEMO
// 执行 throttle 函数返回新函数
const betterFn = throttle(() => {
  isClick.value = true;
  myPlayer.value.currentTime(0);
  myPlayer.value.play();
}, 27000);
// 每 10 毫秒执行一次 betterFn 函数，但是只有时间差大于 1000 时才会执行 fn

const bgClick = () => {
  // betterFn();
  if(myPlayer.value){
    isClick.value = true;
  myPlayer.value.currentTime(0);
  myPlayer.value.play();
 
  } else {
    // 重新绑定事件
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
    // isClick.value = false;
    // isClick2.value = true;
  })
  // 监听播放器播放结束事件
  myPlayer.value.on("ended", function () {
    // 打印日志信息
    console.log("eee");
    // 将isClick的值设为false
    isClick.value = false;
    isClick2.value = true;
    myPlayer.value.dispose;
  });
  }

};
const menuClick = (x) => {
  visible.value = true;
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
      break;
    default:
      break;
  }
};
const handleCancel = () => {
    // 取消操作，将visible值设为false
  visible.value = false;
};
const handleOk = () => {
  // 确定操作，将visible值设为false
  visible.value = false;
};
const videoClick = () => {
  // 清除videojs函数创建的视频播放器
  myPlayer.value.dispose()
  // 将第图层重新切换为第一个图层
  isClick2.value = false;
  isClick.value = false;
  
};
</script>

<template>
  <!--@click="bgClick"-->
  <div class="con">
    <div :class="!isClick ? 'absolute z-999' : 'absolute'">
      <img
        @click.prevent="bgClick"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 75%; left: 47%"
      />
      <!-- <img class="absolute z-999" :src="btn" width="140" height="140"/>
      <img class="absolute z-999" :src="btn" width="140" height="140"/>
      <img class="absolute z-999" :src="btn" width="140" height="140"/>
      <img class="absolute z-999" :src="btn" width="140" height="140"/> -->
      <img
        @click.stop="menuClick(1)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 72%; left: 25%"
      />
      <img
        @click.stop="menuClick(2)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 16%; left: 30%"
      />
      <img
        @click.stop="menuClick(3)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 84%; left: 25%"
      />
      <img
        @click.stop="menuClick(4)"
        class="absolute anima"
        :src="btn"
        width="60"
        height="60"
        style="top: 5%; left: 30%"
      />
      <img
        :src="bgPoster"
        class="!w-full !h-full !max-w-full !max-h-full !min-h-full !min-w-full"
      />
    </div>
    <video
    @click="videoClick"
      ref="videoPlayer"
      :class="
        isClick
          ? 'absolute z-999 video-js !min-h-full !min-w-full !max-w-full !max-h-full !w-full !h-full !object-cover'
          : 'absolute video-js !min-h-full !min-w-full !max-w-full !max-h-full !w-full !h-full !object-cover'
      "
     
      webkit-playsinline="webkit-playsinline"
      playsinline="playsinline"
    ></video>
    <a-modal
      :visible="visible"
      @ok="handleOk"
      :closable="false"
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

    <div :class="isClick2 ? ' absolute z-999 threePage' : 'absolute  bgPoster'">
      <img
        @click="menuClick(1)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 72%; left: 25%"
      />
      <img
        @click.stop="menuClick(2)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 16%; left: 30%"
      />
      <img
        @click.stop="menuClick(3)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 84%; left: 25%"
      />
      <img
        @click.stop="menuClick(4)"
        :src="btn"
        width="60"
        height="60"
        class="anima"
        style="top: 5%; left: 30%"
      />
      <div>
        <a-modal
          v-model:visible="visible2"
          @ok="handleOk"
          :closable="false"
          @cancel="handleCancel"
          :mask-style="maskStyle"
          :modal-style="TabStyle1"
          :footer="false"
          :hide-title="true"
        >
          <div>
            <h1>机场总面积20.2平方千米</h1>
            <a-image :src="message" width="100%" height="100%"></a-image>
          </div>
        </a-modal>
      </div>
      <a-modal
        :visible="visible"
        @ok="handleOk"
        :closable="false"
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
    </div>
    <div :class="isClick2 ? ' absolute z-999 ' : 'absolute  bgPoster'">
      <img
          @click="menuClick(1)"
          :src="btn"
          width="60"
          height="60"
          class="anima"
          style="top: 72%; left: 25%"
      />
      <img
          @click.stop="menuClick(2)"
          :src="btn"
          width="60"
          height="60"
          class="anima"
          style="top: 16%; left: 30%"
      />
      <img
          @click.stop="menuClick(3)"
          :src="btn"
          width="60"
          height="60"
          class="anima"
          style="top: 84%; left: 25%"
      />
      <img
          @click.stop="menuClick(4)"
          :src="btn"
          width="60"
          height="60"
          class="anima"
          style="top: 5%; left: 30%"
      />
      <div>
        <a-modal
            v-model:visible="visible2"
            @ok="handleOk"
            :closable="false"
            @cancel="handleCancel"
            :mask-style="maskStyle"
            :modal-style="TabStyle1"
            :footer="false"
            :hide-title="true"
        >
          <div>
            <h1>机场总面积20.2平方千米</h1>
            <a-image :src="message" width="100%" height="100%"></a-image>
          </div>
        </a-modal>
      </div>
      <a-modal
          :visible="visible"
          @ok="handleOk"
          :closable="false"
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
    </div>
  </div>
</template>

<style>
.con {
  position: relative;

  width: 100% !important;
  height: 100% !important;
  overflow: hidden;
}

.vjs-poster img {
  width: 100% !important;
  height: 100% !important;
  object-fit: fill !important;
}

.threePage {
  background-image: url(./assets/three.png);
  position: fixed;
  width: 100%;
  height: 100%;
  background-size: 100% 100%;
}
.threePage img {
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
