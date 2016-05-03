---
title: 3dTouch
date: 2016-05-03 14:06:29
tags: [3DTouch,IOS]
---

# Getting start

## Home screen quick actions
3D Touch 能够在Home界面的图标上，通过按压在图标的周围显示一个快捷操作（shortcuts）的菜单，通过这个菜单，我们能够更加快速直接的进入某项功能。
如

![](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/Adopting3DTouchOniPhone/Art/maps_directions_home_2x.png)

这种快捷操作（shortcuts）分两种：

* Static shortcuts 静态的，在Info.plist里面配置，在程序安装后就会存在。
* Dynamic shortcuts 动态的，在运行时创建的，直到程序第一次运行后才会存在。


### Static shortcuts


1、 在Info.plist 进行配置 UIApplicationShortcutItems

![](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Art/UIApplicationShortcutItems_plist_editor_2x.png)


2、 实现对应的点击事件
在Appdelegate.m中实现
 
```
-(void)application:(UIApplication *)application performActionForShortcutItem:(UIApplicationShortcutItem *)shortcutItem completionHandler:(void (^)(BOOL))completionHandler
{
    completionHandler(YES);
}
```
### Dynamic shortcuts

```
UIMutableApplicationShortcutItem * itme = [[UIMutableApplicationShortcutItem alloc]initWithType:@"com.yc-ai.Touch3D.sousuo" localizedTitle:@"搜索"];
        
application.shortcutItems = @[itme];

```
>Keys for Home screen quick actions, also known as shortcut items

>UIApplicationShortcutItemType(required)  必须的key 用于区分quick actions
>UIApplicationShortcutItemTitle(required) 用于显示名称
>UIApplicationShortcutItemSubtitle        用于显示子标题
>UIApplicationShortcutItemIconType        图标类型

```
typedef enum UIApplicationShortcutIconType : NSInteger {
   UIApplicationShortcutIconTypeCompose,
   UIApplicationShortcutIconTypePlay,
   UIApplicationShortcutIconTypePause,
   UIApplicationShortcutIconTypeAdd,
   UIApplicationShortcutIconTypeLocation,
   UIApplicationShortcutIconTypeSearch,
   UIApplicationShortcutIconTypeShare,
   UIApplicationShortcutIconTypeProhibit,
   UIApplicationShortcutIconTypeContact,
   UIApplicationShortcutIconTypeHome,
   UIApplicationShortcutIconTypeMarkLocation,
   UIApplicationShortcutIconTypeFavorite,
   UIApplicationShortcutIconTypeLove,
   UIApplicationShortcutIconTypeCloud,
   UIApplicationShortcutIconTypeInvitation,
   UIApplicationShortcutIconTypeConfirmation,
   UIApplicationShortcutIconTypeMail,
   UIApplicationShortcutIconTypeMessage,
   UIApplicationShortcutIconTypeDate,
   UIApplicationShortcutIconTypeTime,
   UIApplicationShortcutIconTypeCapturePhoto,
   UIApplicationShortcutIconTypeCaptureVideo,
   UIApplicationShortcutIconTypeTask,
   UIApplicationShortcutIconTypeTaskCompleted,
   UIApplicationShortcutIconTypeAlarm,
   UIApplicationShortcutIconTypeBookmark,
   UIApplicationShortcutIconTypeShuffle,
   UIApplicationShortcutIconTypeAudio,
   UIApplicationShortcutIconTypeUpdate 
} UIApplicationShortcutIconType;

```
>UIApplicationShortcutItemIconFile 自定义图片文件 ***icons should be square, single color, and 35x35 points*** 
>UIApplicationShortcutItemUserInfo 设置字典信息用于传值


## Peeking and popping

## 在列表页面

* 注册代理

```
[self registerForPreviewingWithDelegate:self sourceView:self.view];
```

* 实现UIViewControllerPreviewingDelegate代理

```
- (nullable UIViewController *)previewingContext:(id <UIViewControllerPreviewing>)previewingContext viewControllerForLocation:(CGPoint)location


{
    NSIndexPath * indexPath = [_tableView indexPathForRowAtPoint:location];
    UITableViewCell * celll = [_tableView cellForRowAtIndexPath:indexPath];
    DetailViewController * detail = [[DetailViewController alloc]init];
    detail.number =_list[indexPath.row];
    previewingContext.sourceRect = celll.frame;
    
    return detail;
    
}
- (void)previewingContext:(id <UIViewControllerPreviewing>)previewingContext commitViewController:(UIViewController *)viewControllerToCommit{

    [self showViewController:viewControllerToCommit sender:self];
    
}
```

## 在详情页面实现

```
- (NSArray<id<UIPreviewActionItem>> *)previewActionItems{
    
    UIPreviewAction * shareAction = [UIPreviewAction actionWithTitle:@"分享" style:UIPreviewActionStyleDefault handler:^(UIPreviewAction * _Nonnull action, UIViewController * _Nonnull previewViewController) {
        
    }];
    
    
    return @[shareAction];

}
```

# [代码](https://github.com/wpfcool/3DTouch.git)

