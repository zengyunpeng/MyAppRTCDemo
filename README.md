# AppRTCDemo

Android Studio project for AppRTCDemo of WebRTC project.


This project now uses [the official prebuilt library](https://bintray.com/google/webrtc/google-webrtc) at jCenter

视频对讲P2P价格:
100台5W块钱,平均一台500块钱

视频对讲API调用流程:

CallActivity :: appRtcClient.connectToRoom(roomConnectionParameters);
-->请求http接口  https://appr.tc/join/733641499
WebSocketRTCClient :: connectToRoomInternal() :: new RoomParametersFetcher(connectionUrl, null, callbacks).makeRequest()
-->获取到信令服务器地址,turn服务器地址,SDP 下面走到回调
onSignalingParametersReady :: WebSocketRTCClient.this.signalingParametersReady(params);
-->
// 创建视频对讲的P2P通道
events.onConnectedToRoom(signalingParameters);

// 连接到基于webSocket的信令服务器
wsClient.connect(signalingParameters.wssUrl, signalingParameters.wssPostUrl);
wsClient.register(connectionParameters.roomId, signalingParameters.clientId);