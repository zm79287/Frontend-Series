# 数据存储

## File\(文件型\)

### FileBrowser

#### [Swift-FileBrowser](https://github.com/marmelroy/FileBrowser)

![](https://camo.githubusercontent.com/5ea19d119a5426eeca3edbe750c280617f804aa0/687474703a2f2f692e67697068792e636f6d2f336f3667615936794c516b686a696f6b35572e676966)

## Cache\(缓存型\)

### NSUserDefault

类似于Android中的SharedPreference以及Web的LocalStorage，iOS中也提供了便捷的可持久化的存储方案：NSUserDefault。NSUserDefault更多的表现像个属性列表，可以看做plist文件的封装好的接口。NSUserDefaults中主要可以存放以下六类接口：

* NSData
* NSString
* NSNumber
* NSDate
* NSArray
* NSDictionary

#### WriteData\(写入数据\)

创建一个user defaults方法有多个，最简单得快速创建方法:

```text
NSUserDefaults *accountDefaults = [NSUserDefaults standardUserDefaults];
//添加数据到 user defaults:
[accountDefaults setObject:nameField.text forKey:UserDefaultNameKey];
```

也可以添加基本数据类型int, float, bool等，有相应得方法

```text
[accountDefaults setBool:YES forKey:UserDefaultBoolKey];
```

如果是Swift，用法如下：

```swift
let defaults = NSUserDefaults.standardUserDefaults()
defaults.setObject("Coding Explorer", forKey: "userNameKey")
```

#### ReadData\(读取数据\)

从UserDefault中读取数据，方式就像从一个全局的Dictionary中读取数据：

```text
 [accountDefaults objectForKey:NCUserDefaultNameKey]
 [accountDefaults boolForKey: UserDefaultBoolKey];
```

如果是Swift，读取方式如下所示：

```swift
let defaults = NSUserDefaults.standardUserDefaults()
if let name = defaults.stringForKey("userNameKey")
{
    println(name)
}
```

## CoreData

## SQLite

### [FMDB](https://github.com/ccgus/fmdb)

### [SQLite.swift](https://github.com/stephencelis/SQLite.swift)

![SQLite.playground Screen Shot](https://github.com/stephencelis/SQLite.swift/raw/master/Documentation/Resources/playground@2x.png)

## Realm

#### Primary Keys

```text
@interface Dog : RLMObject
@property int key;
@property NSString *name;
@property NSInteger age;
@end

@implementation Dog : RLMObject
+ (NSString *)primaryKey {
    return @"key";
}
@end

RLM_ARRAY_TYPE(Dog)

@interface Owner : RLMObject
@property int key;
@property NSString *name;
@property RLMArray<Dog> *dogs;
@end

@implementation Owner : RLMObject
+ (NSString *)primaryKey {
    return @"key";
}
@end
```

在插入数据时，如果发现主键中数据存在重复的则会抛出异常：

```text
Owner *owner = [Owner createOrUpdateInDefaultRealmWithObject:@{
    @"key": @0,
    @"name": @"Tim",
    @"dogs": @[
        @{@"key": @5, @"name": @"Rex", @"age": @3}
    ]
}];

NSLog(@"Number of owners: %u", (unsigned)[Owner allObjects].count);
NSLog(@"Number of dogs: %u", (unsigned)owner.dogs.count);
for (Dog *dog in owner.dogs) {
    NSLog(@"Dog %@", dog);
}
```
