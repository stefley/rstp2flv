## html5中播放rtsp流实现监控demo
 ### 解决方案：`node + ffmpeg + websocket + flv.js`
    0.在node服务中建立websocket
    1.通过fluent-ffmpeg转码，将RTSP 流转为flv格式
    2.前端通过flv.js连接websocket，并对获取的flv格式视频数据进行渲染播放

### node服务相关依赖 (相关代码: server/index.js)
    0.ws
    1.websocket-stream
    2.fluent-ffmpeg
    3.@ffmpeg-installer/ffmpeg

### 前端相关 (相关代码: src/components/HelloWorld.vue)
    0.flv.js

### demo启动流程
    0.npm run dev || yarn dev 启动前端项目
    1.npm run ws || yarn ws 启动nodejs的websocket服务
    2.修改前端代码部分的url为可以正常观看的rstp流地址

### *注意事项*
    0.node转流服务部署服务器需要安装ffmpeg软件用来将rstp转为flv流
    1.demo只是基本实现功能，运用到生产环境时，可进一步完善代码细节，增加代码健壮性
    2.如果需要同时打开多个监控或直播画面，前端多实例化几个flvjs，挂载到video元素上即可

