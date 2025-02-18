# Error Codes and Warning Codes

When you make an API call to access an Agora SDK, the SDK may return error codes or warning codes: **Error codes** are returned when a problem that cannot be recovered without app intervention has occurred. **Warning codes** are returned when a problem that might be resolved automatically has occurred. Warning codes provide information but normally do not require any action.

This article provides descriptions and troubleshooting tips for common Agora SDK error and warning codes. If you receive a response that is not included here, Agora recommends you [submit a ticket](https://agora-ticket.agora.io/) so that our technical support team can help resolve the issue.

<div class="alert note">An error code can be a negative number. In such a case, it should be read as if it were positive. For example, if the SDK returns error code <code>-2</code>, you should refer to <code>2</code> in the error code table.</div>

The error and warning codes may be returned in the following ways:

- The return value of a method call, represented by a negative number. In such a case, it should be read as if it were positive.
- An [onError] or [onWarning] callback.

## General errors

<style> table th:first-of-type {     width: 60px; } </style>

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `0` | No error occurs. |
| `1` | A general error occurs (no specified reason). Try calling the method again. |
| `2` | An invalid parameter is used. For example, the specified channel name includes illegal characters. Please reset the parameters. |
| `3` | The SDK is not ready. Possible reasons:<ul><li>[IRtcEngine] fails to initialize. Please re-initialize [IRtcEngine].</li><li>No user has joined the channel when the method is called. Please check your code logic.</li><li>Users have not left the channel when the [rate] and [complain] methods are called. Please check your code logic.</li><li>The audio module is disabled.</li><li>The program is not complete.</li></ul> |
| `4` | [IRtcEngine] does not support the request. Possible reasons:<ul><li>The [setBeautyEffectOptions] method is called on devices running versions earlier than Android 4.4. Please check the Android version.</li><li>The built-in encryption mode is incorrect or the SDK fails to load the external encryption library. Please check the encryption mode setting or reload the external encryption library.</li></ul> |
| `5` | The request is rejected. Possible reasons:<ul><li>[IRtcEngine] fails to initialize. Please re-initialize [IRtcEngine].</li><li>The channel name is set as the empty string "" when creating the [IChannel] instance. Please reset the channel name.</li><li>When the [joinChannel2] method is called to join one of multiple channels, the specified channel name is already in use. Please reset the channel name.</li><li>The `joinChannel` method in [IRtcEngine] is called to join another channel after an [IChannel] instance has been created to join a channel and a stream has been published in the channel. The `joinChannel` method in [IRtcEngine] is called to join another channel after an [IChannel] instance has been created to join a channel and a stream has been published in the channel.</li><li>A user whose role is not audience calls the [switchChannel2] method. Ensure that the user role is audience before calling the `switchChannel` method.</li></ul> |
| `6` | The buffer size is insufficient to store the returned data. |
| `7` | ]IRtcEngine[ is not initialized. Ensure that the [IRtcEngine] instance is created and initialized before calling the method. |
| `9` | Permission to access is not granted. Check whether your app has access to the audio and video device. |
| `10` | A timeout occurs. Some API calls require the SDK to return the execution result. This error occurs if the SDK takes too long (more than 10 seconds) to return the result. |
| `17` | The request to join the channel is rejected. Typical reasons include:<ul><li>The user is already in the channel and still calls a method (for example, [joinChannel2]) to join the channel. Stop calling this method to clear this error.</li><li>The user tries to join a channel during a call test started by calling [startEchoTest2]. To join a channel, the call test must be ended by calling [stopEchoTest].</li></ul> |
| `18` | The request to leave the channel is rejected. Typical reasons include:<ul><li>The user has left the channel but still calls a method (for example, [leaveChannel]) to leave the channel. Stop calling this method to clear this error.</li><li>The user is not in the channel and calls a method to leave the channel. In this case, no extra operation is needed.</li></ul> |
| `19` | Resources are already in use. |
| `20` | The request is abandoned by the SDK, possibly because the request has been sent too frequently. |
| `21` | ]IRtcEngine[ fails to initialize and has crashed because of specific Windows firewall settings. |
| `22` | The SDK fails to allocate resources because your app uses too many system resources or system resources are insufficient. |
| `101` | The specified App ID is invalid. Please rejoin the channel with a valid App ID. |
| `102` | The specified channel name is invalid, possibly because the data types of some parameters are incorrect. Please rejoin the channel with a valid channel name. |
| `103` | Fails to get server resources in the specified region. Try another region when initializing [IRtcEngine]. |
| `109` | **Note**: This method is deprecated as of v2.4.1. Please use [CONNECTION_CHANGED_TOKEN_EXPIRED]\(9) in the [onConnectionStateChanged] callback instead. </br>The current token has expired. Please apply for a new token on the server and call [renewToken]. |
| `110` | **Note**: This method is deprecated as of v2.4.1. Please use [CONNECTION_CHANGED_INVALID_TOKEN]\(8) in the [onConnectionStateChanged] callback instead. </br>The token is invalid. Typical reasons include:<ul><li>App Certificate is enabled in Agora Console, but the code still uses App ID for authentication. Once App Certificate is enabled for a project, you must use token-based authentication.</li><li>The user ID used to generate the token is not the same as the one used to join the channel.</li></ul> |
| `111` | The network connection is interrupted. This error occurs when the SDK has connected to the server but lost connection for more than 4 seconds. |
| `112` | The network connection is lost.  This error occurs when the connection is interrupted and the SDK cannot reconnect to the server within 10 seconds. |
| `113` | The user is not in the channel when calling the method. |
| `114` | The data size exceeds 1024 bytes when calling the [sendStreamMessage] method. |
| `115` | The data bitrate exceeds 6 Kbps when calling the [sendStreamMessage] method. |
| `116` | More than five data streams are created when calling the [createDataStream2] method. |
| `117` | The data stream transmission times out. |
| `119` | Switching roles fails. |
| `120` | Decryption fails. The user may have entered an incorrect password to join the channel. Check the entered password or tell the user to try rejoining the channel. |
| `123` | The user is banned from the server. This error occurs when the user is kicked out of the channel from the server. |
| `134` | The user account is invalid, possibly because it contains invalid parameters. |


## Watermark errors

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `124` | Incorrect watermark file parameter. |
| `125` | Incorrect watermark file path. |
| `126` | Incorrect watermark file format. The SDK only supports adding PNG files as the watermark image. |
| `127` | Incorrect watermark file information. |
| `128` | Incorrect watermark file data format. |
| `129` | An error occurs when reading the watermark file. |


## Streaming errors

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `130` | Stream encryption is enabled when the user calls the [addPublishStreamUrl] method. The SDK does not support pushing encrypted streams to CDN. |
| `151` | An error occurs when pushing streams to CDN. Please remove the current URL address by calling the [removePublishStreamUrl] method, and then add a new address by calling the [addPublishStreamUrl] method. |
| `152` | The host has published more than 10 URLs. Please delete the unnecessary URLs before adding new ones. |
| `153` | The host is making changes to other hosts' URLs, such as updating parameters and disabling a URL. Please check your app logic. |
| `154` | An error occurs in Agora's streaming server. Call the [addPublishStreamUrl] method to push the stream again. |
| `155` | The server fails to find the stream. |
| `156` | The URL format is incorrect. Check whether the URL format is correct. |

## Audio errors

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `1005` | A general error occurs (no specified reason). Check whether the audio device is already in use by another app, or try rejoining the channel. |
| `1006` | An error occurs when using Java resources. Check whether the audio device storage is sufficient, or restart the audio device. |
| `1007` | The sampling frequency setting is incorrect. |
| `1008` | An error occurs when initializing the playback device. Check whether the playback device is already in use by another app, or try rejoining the channel. |
| `1009` | An error occurs when starting the playback device. Check the playback device, or try rejoining the channel. |
| `1010` | An error occurs when stopping the playback device. |
| `1011` | An error occurs when initializing the recording device. Check the recording device, or try rejoining the channel. |
| `1012` | An error occurs when starting the recording device. Check the recording device, or try rejoining the channel. |
| `1013` | An error occurs when stopping the recording device. |
| `1015` | A playback error occurs. Check the playback device, or try rejoining the channel. |
| `1017` | A recording error occurs. Check the recording device, or try rejoining the channel. |
| `1018` | Recording fails. |
| `1022` | An error occurs when initializing the loopback device. |
| `1023` | An error occurs when starting the loopback device. |
| `1027` | Permission to record is not granted. Check whether permission to record is granted or whether the recording device is already in use by another app. |
| `1033` | The recording device is already in use. |
| `1101` | An error occurs when using Java resources. Check whether the audio device storage is sufficient, or restart the audio device. |
| `1108` | The audio recording frequency is lower than 50 Hz. In this case, the frequency is often 0, which indicates that the recording has not started. Agora recommends that you check whether permission to record is granted. |
| `1109` | The audio playback frequency is lower than 50 Hz. In this case, the frequency is often 0, which indicates that the playback has not started. Agora recommends that you check whether too many AudioTrack instances have been created. |
| `1111` | Recording fails to start, and a ROM system error occurs. Possible solutions: Restart your app. Restart the device on which your app is running. Check whether permission to record is granted. |
| `1112` | Playback fails to start and a ROM system error occurs. Possible solutions: Restart the app. Restart the device on which your app is running. Check whether permission to record is granted. |
| `1115` | Recording fails. Check whether there is permission to record or whether there is a problem with the network connection. |
| `1201` | The current device does not support audio input, possibly because the configuration of the Audio Session category is incorrect, or because the device is already in use. Agora recommends terminating all background apps and rejoining the channel. |
| `1206` | Audio Session fails to launch. Check your recording settings. |
| `1210` | An error occurs when initializing the playback device. An error occurs when initializing the audio device, usually because some audio device parameters are incorrect. |
| `1213` | An error occurs when re-initializing the playback device. An error occurs when initializing the audio device, usually because some audio device parameters are incorrect. |
| `1214` | An error occurs when restarting the playback device. An error occurs when restarting the audio device, usually because the Audio Session category setting is not compatible with the audio device settings. |
| `1301` | The audio device module fails to initialize. Disable and re-enable the audio device, or restart the device on which your app is running. |
| `1303` | The audio device module fails to terminate. Disable and re-enable the audio device, or restart the device on which your app is running. |
| `1306` | The playback device fails to initialize. Disable and re-enable the audio device, or restart the device on which your app is running. |
| `1307` | Initialization fails because no audio playback device is available. Ensure that a proper audio device is connected. |
| `1309` | Recording fails to start. Disable and re-enable the audio device, or restart the device on which your app is running. |
| `1311` | The system fails to create a recording thread, possibly because the device storage or performance is insufficient. Restart the device or use a different one. |
| `1314` | Recording fails to start. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1319` | The system fails to create a playback thread, possibly because the device storage or performance is insufficient. Restart the device or use a different one. |
| `1320` | Audio playback fails to start. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1322` | No recording device is available. Ensure that a proper audio device is connected. |
| `1323` | No playback device is available. Ensure that a proper audio device is connected. |
| `1351` | The audio device module fails to initialize. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1353` | The recording device fails to initialize. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1354` | The microphone fails to initialize. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1355` | The playback device fails to initialize. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1356` | The speaker fails to initialize. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1357` | Recording fails to start. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1358` | Audio playback fails to start. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1359` | No recording device is available. Check whether the recording device is connected or whether it is already in use by another app. |
| `1360` | No playback device is available. Check whether the playback device is connected or whether it is already in use by another app. |
| `1735` | The Windows Audio service is disabled. You need to either enable the Windows Audio service or restart the device. |

## Video errors

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `1003` | **Note**: This method is deprecated as of v2.4.1. Please use [LOCAL_VIDEO_STREAM_ERROR_CAPTURE_FAILURE]\(4) in the [onLocalVideoStateChanged] callback instead. </br>The camera fails to start. Check whether the camera is already in use by another app, or try rejoining the channel. |
| `1004` | The video rendering module fails to start. |
| `1510` | Permission to access the camera is not granted. Check whether permission to access the camera permission is granted. |
| `1512` | **Note**: This method is deprecated as of v2.4.1. Please use [LOCAL_VIDEO_STREAM_ERROR_DEVICE_BUSY]\(3) in the [onLocalVideoStateChanged] callback instead. </br>The camera is already in use. |
| `1600` | An unknown error occurs. |
| `1601` | Video encoding initialization fails. Try rejoining the channel. |
| `1602` | Video encoding fails. Try rejoining the channel. |
| `1603` | Video encoding settings fail to be applied. |
| `1736` | The SDK does not support you to set `excludeWindowList` to block windows on a device with multiple graphics cards. |


## Other errors

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `1001` | The SDK fails to load the media engine. |
| `1002` | The SDK fails to start an audio/video call after launching the media engine. Try rejoining the channel. |


## Warning code

| Enumerator | Description |
| :----- | :----------------------------------------------------------- |
| `8` | The specified view is invalid. The video call function requires a specified view. |
| `16` | The SDK fails to initialize the video call function, possibly due to a lack of resources. When this warning occurs, users cannot make a video call, but the voice call function is not affected. |
| `20` | The request is pending, usually because some modules are not ready, causing the SDK to postpone processing the request. |
| `103` | 103: No channel resources are available. Maybe because the server cannot allocate any channel resource. |
| `104` | A timeout occurs when the SDK is searching for a specified channel. When receiving a request to join a channel, the SDK searches for the channel first. This warning usually occurs when the network connection is too poor for the SDK to connect to the server. |
| `105` | **Note**: This method is deprecated as of v2.4.1. Please use [CONNECTION_CHANGED_REJECTED_BY_SERVER]\(10) in the [onConnectionStateChanged] callback instead. </br>105: The server rejected the request to look up the channel. The server cannot process this request or the request is illegal. |
| `106` | A timeout occurs when joining the channel. Once the specified channel is found, the SDK starts joining the channel. This warning usually occurs when the network connection is too poor for the SDK to connect to the server. |
| `107` | 105: The server rejected the request to look up the channel. The server cannot process this request or the request is illegal. |
| `111` | A timeout occurs when switching to the live video. |
| `118` | A timeout occurs when setting user roles in the live-streaming profile. |
| `121` | The ticket to join the channel is invalid. |
| `122` | The SDK is trying to connect to another server. |
| `131` | The channel connection cannot be recovered. |
| `132` | The IP address has changed. |
| `133` | The port has changed. |
| `701` | An error occurs when opening the audio-mixing file. |
| `1014` | A playback device warning occurs. |
| `1016` | A recording device warning occurs. |
| `1019` | No data is recorded. Possible solutions: Check whether the microphone is already in use. Check whether permission to record is granted. Check whether the recording device works properly. Restart the device. |
| `1020` | The audio playback frequency is abnormal due to high CPU usage. Recommended solutions: Close other apps that are consuming CPU resources. You can also check whether the audio module is enabled in your app or try rejoining the channel. |
| `1021` | The audio recording frequency is abnormal due to high CPU usage. You can close other apps that are consuming CPU resources. You can also check whether the audio module is enabled in your app or try rejoining the channel. |
| `1025` | The audio playback or recording is interrupted by system events (such as a phone call). |
| `1029` | The Audio Session category must be set as `AVAudioSessionCategoryPlayAndRecord`. During a call, [IRtcEngine] monitors the Audio Session category. If the category is modified, this warning occurs, and the SDK automatically sets it back to `AVAudioSessionCategoryPlayAndRecord`. |
| `1031` | The recording volume is too low. Check whether the user's microphone is muted or whether the user has enabled microphone augmentation. |
| `1032` | The playback volume is too low. Check whether the user's microphone is muted or whether the user has enabled microphone augmentation. |
| `1033` | The recording device is already in use. Check whether permission to record is granted or whether another app is using the device. |
| `1040` | No audio data is available. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1051` | Audio feedback is detected during recording. Ensure that users in the same channel maintain sufficient physical distance between themselves. |
| `1052` | The system threads for recording and playback cannot be arranged due to high CPU usage. |
| `1053` | A residual echo is detected. This may be caused by the delayed scheduling of system threads or a signal overflow. |
| `1323` | No playback device is available. Ensure that a proper audio device is connected. |
| `1324` | The recording device is released improperly. Possible solutions: Disable and re-enable the audio device. Restart the device on which your app is running. Update the sound card driver. |
| `1610` | The original resolution of the remote video is beyond the range (640 × 480) where the super-resolution algorithm can be applied. |
| `1611` | Another user is using super resolution. |
| `1612` | The device does not support super resolution. |