     数联时代FOTA安装包在附件里请查收，如有问题请与我或我们的技术联系。
    一、 FOTA的APK包见附，
    请将其内置到项目的系统目录下：
    1、（ android4.4及更高放到system/priv-app；低于 android4.4的放到 system/app）
    2、（ android5.0版本及以上放置于 system/priv-app ） ，
    5.0版本的SystemFota_5.0.apk 需进行系统签名！
    [签名方法：1、把SystemFota.apk里面的META-INF删除，可以直接用解压软件打开删除
    2、使用命令：java -jar signapk.jar platform.x509.pem platform.pk8 NoSigned.apk Signed.apk 以上 platform.x509.pem platform.pk8 请使用自己工程上相对应的签名文件。signapk.jar 在工程out/host/linux-x86/framework]
    每次量产软件版本，请保留整包以方便制作升级包，整包制作说明见附【整包注意事项】；
    如需支持，请联络：宫庆忠（TEL:13691892867，QQ:524900280）
    
    ./build/target/product/security/platform.x509.pem    userdebug
./build/target/product/security/release/platform.x509.pem

java -jar out/host/linux-x86/framework/signapk.jar build/target/product/security/platform.x509.pem build/target/product/security/platform.pk8 SystemFota1.apk SystemFota.apk



    二、管理后台如下，操作说明见附【FOTA新版后台说明.ppt】
    地址: http://portal.digitimetech.com/signin
    账号: LUOBIN
    密码: 000000
    如需支持，请联络：孙金花（TEL:13714655330，QQ:529502428）

    谢谢！


二、 无icon_入口设置方法：
  可以直接在替换 “设置-->关于手机-->系统升级”  。我们包名：com.system.ftools ，入口activity：
  adb shell am start -n com.fota.wirelessupdate/com.fota.wirelessupdate.activity.MainActivity


    ------------------
    BRs,
    徐东全/Daniel Xu
    手机：13701161710
    E-mail：daniel@digitimetech.com
    深圳市数联时代科技有限公司


整包注意事项.txt

如果制作差分包时 ，请注意以下几点：
1、编译，按以下顺序执行编译
  make [project] new
  make [project] otapackage
 【【【【注意：打包或备份img文件一定要在编译otapackage之后，因为执行otapackage时img文件会重新生成，如果直接在new之后执行打包或备份img会造成手机的源版本与制作差分包的源版本不一致。】】】】
2、文件备份
     请将编译后生成的文件out/target/product/[project]/obj/PACKAGING/target_files_intermediates目录下生成1个xxx-target_files-eng.xxx.zip，与你们的发布版本放到一起备份
3、差分包
     将第2步骤中的zip包复制到目录\android目录下
     执行  ./build/tools/releasetools/ota_from_target_files -i a.zip b.zip  update.zip
     就会生成另外一个zip包
     a.zip 代表上个版本编译后生成的ota包，b.zip 代表当前版本编译后生产的ota包，update.zip就是要生成的差分包


查看版本号方法：
   1）查看版本号 ：一个方法是直接进我们应用，界面上显示的。

   2）另外就是在 system/build.prop里面 
      ro.build.display.id+"."+ro.build.date.utc 

     如：ro.build.display.id = sdk-eng2.2FRF91 
         ro.build.date.utc   = 1277931480
     版本号是: sdk-eng2.2FRF91.1277931480
