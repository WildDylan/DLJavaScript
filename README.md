# DLJavaScript
Study JavaScriptCore And JavaScript

```objective-c
// 创建新的Context
    JSContext * context = [[JSContext alloc] init];
    
    // 执行JS 代码
    [context evaluateScript:@"var num = 5 + 5"];
    [context evaluateScript:@"var names = ['Grace', 'Ada', 'Margaret']"];
    [context evaluateScript:@"var triple = function(value) { return value * 3 }"];
    
    // 直接执行JS代码 并且得到返回结果, 也可以先取到值、再去CallWithArgument或者拿出数组中的数据
    JSValue * tripleNum = [context evaluateScript:@"triple(num)"];
    
    NSLog(@"%d", [tripleNum toInt32]);
    
    // 得到JS里边的一些值、
    JSValue *names = context[@"names"];
    // 从值中取出数据
    JSValue *initialName = names[0];
    
    NSLog(@"The first name: %@", [initialName toString]);
    
    // 得到JS中的一个方法
    JSValue *tripleFunction = context[@"triple"];
    // 使用一个参数 传入到方法中
    JSValue *result = [tripleFunction callWithArguments:@[@5] ];
    
    NSLog(@"Five tripled: %d", [result toInt32]);
    
    // 异常通过JSValue的方式抛出、
    [context setExceptionHandler:^(JSContext * context, JSValue * exception) {
       
        NSLog(@"JS Error: %@", exception);
    }];
    
    // 执行一句错误的JS代码、 以便我们抛出异常
    [context evaluateScript:@"function multiply(value1, value2) { return value1 * value2 "];
    
    // Throw exception
    NSArray * array = [NSArray arrayWithObjects:@"1", @"2", nil];
    @try {
        
        NSInteger excep = [array[5] integerValue] + [array[10] integerValue];
        NSLog(@"%ld", excep);
    }
    @catch (NSException *exception) {
        @throw exception;
    }
    @finally {
        
    }
```

`Let's Fix Bug...`
