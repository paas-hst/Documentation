# 加入组
登录和加入组是两个动作，登录成功后才能加入组。大部分业务需要加入组后才能正常使用

## 如何登录

## 如何加入组

登录成功后，调用加入组的方法即可加入组：
'''
pFspEngine->JoinGroup(szGroupId);
'''

加入成功或失败的结果，通过回调 OnFspEvent 方法回调， eventType == EVENT_JOINGROUP_RESULT