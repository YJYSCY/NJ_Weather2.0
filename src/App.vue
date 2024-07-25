<template>
  <div>
    <div class="header">
      <div class="header_left">
        <template>
          <el-form
            size="mini"
            :inline="true"
            ref="form"
            class="demo-form-inline"
          >
            <el-form-item label="所在南京地区">
              <el-select
                v-model="form.address"
                placeholder="请选择所在南京地区"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
            </el-form-item>
          </el-form>
        </template>
      </div>
      <div class="header_center">
        <h4 style="margin-left: 100px">
          更新时间：<span style="color: blue">{{
            this.weatherData[0].reporttime
          }}</span>
        </h4>
        <ul style="display: flex; width: 600px; margin-top: 10px">
          <li style="flex: 1; display: inline-block">
            所在地区：{{ this.weatherData[0].city }}
          </li>
          <li style="flex: 1; display: inline-block">
            当前天气：{{ this.weatherData[0].weather }}
          </li>
          <li style="flex: 1; display: inline-block">
            当前气温：{{ this.weatherData[0].temperature }}
          </li>
        </ul>
        <ul style="display: flex; width: 600px; margin-top: 10px">
          <li style="flex: 1; display: inline-block">
            风向：{{ this.weatherData[0].winddirection }}
          </li>
          <li style="flex: 1; display: inline-block">
            风力：{{ this.weatherData[0].windpower }}级
          </li>
          <li style="flex: 1; display: inline-block">
            空气湿度：{{ this.weatherData[0].humidity }}
          </li>
        </ul>
      </div>
      <!-- <div>
        <a-map-component
          :center="[116.405285, 39.904989]"
          :zoom="13"
        ></a-map-component>
      </div> -->
    </div>
    <div class="body">
      <AMapComponent :jwd="this.form.address"></AMapComponent>
    </div>
    <div class="pictureBody">
      <template>
        <el-carousel :interval="4000" type="card" height="200px">
          <el-carousel-item
            v-for="(image, index) in images"
            :key="index"
            class="carousel-item"
          >
            <el-image
              :src="image"
              class="carousel-image"
              alt="carousel image"
              :preview-src-list="srcList"
            ></el-image>
          </el-carousel-item>
        </el-carousel>
      </template>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import AMapComponent from './components/AMapComponent.vue';
export default {
  components: {
    AMapComponent,
  },
  data() {
    return {
      weatherData: [{ reporttime: '' }],
      apiKey: '29dd514cc560e7d7b6977ef0de5f301b',
      images: [
        'https://www.1231238.xyz/uploadfile/202407/19/5B91929915.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/4591929411.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/E791929216.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/BD91929368.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/C291929971.jpg ',
        'https://www.1231238.xyz/uploadfile/202407/19/F891929501.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/2591929828.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/A591929720.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/8E91929577.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/6E91929876.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/D391929127.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/ED91929991.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/9591929468.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/C291929636.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/8391929901.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/ED91929165.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/3891929315.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/7291929956.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/6791929124.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/DB91929443.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/9391929700.jpg',
      ],
      srcList: [
        'https://www.1231238.xyz/uploadfile/202407/19/5B91929915.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/4591929411.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/E791929216.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/BD91929368.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/C291929971.jpg ',
        'https://www.1231238.xyz/uploadfile/202407/19/F891929501.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/2591929828.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/A591929720.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/8E91929577.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/6E91929876.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/D391929127.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/ED91929991.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/9591929468.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/C291929636.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/8391929901.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/ED91929165.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/3891929315.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/7291929956.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/6791929124.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/DB91929443.jpg',
        'https://www.1231238.xyz/uploadfile/202407/19/9391929700.jpg',
      ],
      options: [
        {
          value: '320102',
          label: '玄武区',
        },
        {
          value: '320115',
          label: '江宁区',
        },
        {
          value: '320111',
          label: '浦口区',
        },
        {
          value: '320104',
          label: '秦淮区',
        },
        {
          value: '320106',
          label: '鼓楼区',
        },
        {
          value: '320105',
          label: '建邺区',
        },
        {
          value: '320113',
          label: '栖霞区',
        },
        {
          value: '320114',
          label: '雨花台区',
        },
        {
          value: '320117',
          label: '溧水区',
        },
        {
          value: '320118',
          label: '高淳区',
        },
        {
          value: '320116',
          label: '六合区',
        },
      ],
      form: {
        address: '',
      },
    };
  },
  created() {},
  methods: {
    sureClick(newVal = null, oldVal = null) {
      if (!this.form.address) {
        alert('请选择所在南京地区！');
        return;
      }
      // 构建请求的URL
      const url = `https://restapi.amap.com/v3/weather/weatherInfo?key=${this.apiKey}&city=${this.form.address}`;
      // 使用axios发送GET请求
      axios
        .get(url)
        .then((response) => {
          // 请求成功，处理响应数据
          if (response.data.status === '1') {
            this.weatherData = response.data.lives; // 假设天气数据在response.data.lives中
            // console.log(this.weatherData); // 正确位置：在数据被成功赋值后打印
          } else {
            console.error('请求天气信息失败：', response.data.info);
          }
        })
        .catch((error) => {
          // 请求失败
          console.error('请求天气信息时发生错误：', error);
        });
      // 移除了无限递归调用
      // 这里是 sureClick 方法的实现
      // 你可以根据 newVal 和 oldVal 来执行一些逻辑
      console.log('地址已更改', newVal, '之前是', oldVal);
      // 注意：这个方法现在也可以被按钮的 @click 事件触发
    },
  },
  watch: {
    // 监听 form.address 的变化
    'form.address'(newVal, oldVal) {
      // 当 form.address 发生变化时，调用 sureClick 方法
      this.sureClick(newVal, oldVal); // 你可以根据需要传递新值和旧值
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.carousel-item {
  /* 移除或调整轮播项的背景色，如果需要的话 */
  background-color: transparent;
  overflow: hidden; /* 确保图片不会溢出轮播项 */
}

.carousel-image {
  /* 尝试使用aspect-ratio，但请注意这需要浏览器支持 */
  aspect-ratio: 1.4; /* 假设图片的宽高比是16:9，根据你的图片进行调整 */
  height: 100%; /* 填满轮播项的高度 */
  width: 100%; /* 如果aspect-ratio不支持，这将覆盖它，但可能导致不正确的宽高比 */
  object-fit: contain; /* 保持图片的宽高比，但可能会留白 */
}

li {
  list-style: none;
}
.header {
  width: 100%;
  height: 100px;
  padding: 10px;
  background: url(./img/111.jpg);
  background-position: center;
  display: flex;
}
.body {
  width: 400;
  height: 400px;
  padding: 10px;
  /* 
  background-color: pink; */
  display: flex;
}
.pictureBody {
  margin-left: 35%;
  margin-top: 20px;
  width: 550px;
  height: 100%;
}
.header_left {
  margin-top: 20px;
  height: 100%;
  flex-grow: 3;
  padding: 0 5px;
}
.header_center {
  height: 100%;
  flex-grow: 7;
  padding: 0 5px;
}
</style>
