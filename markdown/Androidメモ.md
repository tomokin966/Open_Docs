## ツール

adbから任意のActivityを起動したい

https://qiita.com/kikuchy/items/39d1901c7007e37bfe02

→アプリのデバッグに便利そう

adbを15秒でインストールするやつ

https://barihack.net/adb-15sec-install/

→色々よしなにやってくれるから便利

## スクリプト

MacOSに接続したAndroidデバイスでスクリーンショットを取って、デスクトップに置くスクリプト

```bash
cd
rm .bashrc
mkdir -p Desktop/ScreenShots
touch .bashrc

# AndroidSDK path
cat > .bash_profile
export PATH=\$PATH:/Users/`logname`/Library/Android/sdk/platform-tools
_EOF_

cat  .bashrc
# Android ScreenShot Function
function ss() {
	cd;
	device_name=\`adb shell getprop | grep -oE ro\.product\.model.* | sed -e "s/^.*\[//" | sed "s/]//" | sed "s/ /_/g"\`;
	mkdir -p Desktop/ScreenShots/\$device_name/\$1;
	adb shell screencap -p /sdcard/screen.png;
	adb pull /sdcard/screen.png Desktop/ScreenShots/\$device_name/\$1/screen_\`date +%Y%m%d_%H-%M-%S\`.png;
	adb shell rm /sdcard/screen.png;
}
# Android adb Connect Function
function connect(){
	adb disconnect;
	sleep 3s;
	adb kill-server \$;
	wait;
	adb start-server \$;
	wait;
	port="5555"
	adb tcpip \$port;
	sleep 3s;
	adb wait-for-device;
	sleep 2s;
	ipaddr=\`adb shell ip addr show wlan0 | grep -oE 'inet \d+\.\d+\.\d+\.\d+' | grep -oE '\d+\.\d+\.\d+\.\d+'\`;
	adb connect \$ipaddr:\$port;
}
_EOF_

source .bashrc
source .bash_profile
```