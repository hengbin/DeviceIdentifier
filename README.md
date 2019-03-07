# DeviceIdentifier
iOS一直都比较注重用户隐私，在 iOS 5.0之后系统UDID方法就被废弃掉了，iOS 7中mac地址又被封杀，所有获取mac都将返回统一值02:00:00..，虽然iOS 6.0新增了两个用于替换UDID的接口，分别是：identifierForVendor，advertisingIdentifier(有时可能获取不到)，但这两个接口会在相同开发组下的应用删除完后重新安装应用时数值会发生改变，并不是唯一的标示符。经过对钥匙串及iCloud同步的多方面了解，如果通过系统钥匙串保存一串字符串，且不允许它同步到其他设备，这样不就可以生成一个真正意义上的唯一ID了麽，而且还不会被苹果封杀，即使identifierForVendor的值发生了改变它也依然不变，除非执行设备“抹除所有内容和设置”这一项操作。鉴于网上很多类似原理生成唯一ID的资料要么是依赖了SAMKeyChains库，要么是需要加载KeychainItemWrapper类文件，感觉有点麻烦，于是动手封装了以下类，它不需要你加载其它类库，随拷贝随用。