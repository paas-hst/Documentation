# 高级功能

## 设备管理

系统中存在多个音频设备时，通过 IDeviceManager 接口可列举出系统中所有的扬声器，麦克风设备，
每个设备由 device_id 标识。

## 设备拔插事件

SDK内部会监控系统摄像头拔插，并通过 IFspEngineEventHandler::OnDeviceChange 方法回调通知上层拔插的事件。

上层收到事件后可重新获取摄像头列表。

## 音频系统控制

音频控制通过 IAudioEngine 接口实现，通过该接口，可以实现大部分音频控制相关功能：

1. 设置，获取当前扬声器设备
2. 设置，获取当前麦克风设备
3. 获取，设置扬声器，麦克风音量
4. 静音麦克风，扬声器

## 声音能量值

能量值表示说话的声音大小，SDK提供获取能量值的方法：
1. 本地能量值

IAudioEngine::GetAudioParam 方法获取扬声器，或麦克风设备的能量值。

2. 远端能量值

通过 IFspEngine::GetRemoteAudioEnergy 方法可以获取到远端单个用户的音频能量。
