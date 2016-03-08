---
title: 判断ios设备旋转方向
date: 2016-03-8 22:12:57
tags: ios
---

---
title: 判断ios设备旋转方向
date: 2016-03-8 22:12:57
tags: ios
---

* 首先你要在对应的`controller`中，开启旋转的功能

  ```
  // 默认开启全部方向的旋转
  - (BOOL)shouldAutorotate {
      return YES;
  }
  ```

* 下一个方法是可以旋转接受哪几个方向的旋转

  ```
  - (UIInterfaceOrientationMask)supportedInterfaceOrientations {
        return UIInterfaceOrientationMaskPortrait |UIInterfaceOrientationMaskLandscapeLeft;
    }
  ```

  ```
  // 可以选择多个方向选择
  typedef NS_OPTIONS(NSUInteger, UIInterfaceOrientationMask) {
      UIInterfaceOrientationMaskPortrait = (1 << UIInterfaceOrientationPortrait),
      UIInterfaceOrientationMaskLandscapeLeft = (1 << UIInterfaceOrientationLandscapeLeft),
      UIInterfaceOrientationMaskLandscapeRight = (1 << UIInterfaceOrientationLandscapeRight),
      UIInterfaceOrientationMaskPortraitUpsideDown = (1 << UIInterfaceOrientationPortraitUpsideDown),
      UIInterfaceOrientationMaskLandscape = (UIInterfaceOrientationMaskLandscapeLeft | UIInterfaceOrientationMaskLandscapeRight),
      UIInterfaceOrientationMaskAll = (UIInterfaceOrientationMaskPortrait | UIInterfaceOrientationMaskLandscapeLeft | UIInterfaceOrientationMaskLandscapeRight | UIInterfaceOrientationMaskPortraitUpsideDown),
      UIInterfaceOrientationMaskAllButUpsideDown = (UIInterfaceOrientationMaskPortrait | UIInterfaceOrientationMaskLandscapeLeft | UIInterfaceOrientationMaskLandscapeRight),
  } __TVOS_PROHIBITED;
  ```

* 旋转的时候，你可以开启系统通知的功能，这样你就可以在旋转的时候执行特定的函数了

  ```
  [[NSNotificationCenter defaultCenter] addObserver:self
                      selector:@selector(statusBarOrientationChange:)                                                               name:UIApplicationDidChangeStatusBarOrientationNotification
                                               object:nil];

   // 打印出相关的方向
   - (void)statusBarOrientationChange:(NSNotification *)notification {

      UIInterfaceOrientation oriention = [UIApplication sharedApplication].statusBarOrientation;
      NSLog(@"%ld",(long)oriention);
  }
  ```

