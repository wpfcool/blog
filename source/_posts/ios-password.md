---
title: 仿支付宝密码框
date: 2020-08-04 18:50:50
tags: [iOS]
---



### 使用UIKeyInput实现

#### UIKeyInput协议主要方法

```objective-c
@protocol UIKeyInput <UITextInputTraits>

- (BOOL)hasText;// A Boolean value that indicates whether the text-entry objects has any text. (required)YES
 //if the backing store has textual content, NO otherwise. 官方文档的解释我也翻译不好 
- (void)insertText:(NSString *)text;// 插入文本
- (void)deleteBackward; // 键盘上的退格事件
@end
```

### 简单实现

```objective-c
@interface PasswordView : UIView<UIKeyInput>
@property (nonatomic,assign)NSInteger maxLength;
@end


//
//  PasswordView.m
//  Lock
//
//  Created by mac on 2020/8/4.
//  Copyright © 2020 shandongwenyuan. All rights reserved.
//

#import "PasswordView.h"
@interface PasswordView()
@property (nonnull,strong)NSMutableString *textStore;
@end
@implementation PasswordView

- (instancetype)initWithCoder:(NSCoder *)coder
{
    self = [super initWithCoder:coder];
    if (self) {
        _maxLength = 6;
        _textStore = [NSMutableString string];
    }
    return self;
}

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        _maxLength = 6;
        _textStore = [NSMutableString string];


    }
    return self;
}

-(BOOL)hasText{
    return self.textStore.length>0;
}
- (void)insertText:(NSString *)text{
    if(self.textStore.length < self.maxLength){
        [self.textStore appendString:text];
        [self setNeedsDisplay];
    }

}
- (void)deleteBackward{
     if (self.textStore.length > 0) {

        [self.textStore deleteCharactersInRange:NSMakeRange(self.textStore.length - 1, 1)];

      }

      [self setNeedsDisplay];


}

- (BOOL)canBecomeFirstResponder{
    return YES;
}

- (UIKeyboardType)keyboardType{
    return UIKeyboardTypePhonePad;
}

// Only override drawRect: if you perform custom drawing.
// An empty implementation adversely affects performance during animation.
- (void)drawRect:(CGRect)rect {
    // Drawing code
    
    CGFloat width = rect.size.width;
    CGFloat height = rect.size.height;
    CGContextRef context = UIGraphicsGetCurrentContext();
    CGContextSetFillColorWithColor(context, RGB(0xf7f7f7).CGColor);
    CGFloat item_width = (width-10*self.maxLength-1)/self.maxLength;
    for (int i = 0; i < self.maxLength; i++) {
        //画边框
        CGContextFillRect(context, CGRectMake(i*(item_width+10), 0, item_width, height));
        
    }
    CGContextSetFillColorWithColor(context,[UIColor blackColor].CGColor);

    for (int  i = 0; i < self.textStore.length; i++) {
        
        CGContextAddArc(context,i*(item_width+10)+item_width/2.0, height/2.0, 5, 0, M_PI*2, YES);
        CGContextDrawPath(context, kCGPathFill);
        
    }
    
}


@end

```

