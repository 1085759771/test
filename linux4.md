# linux homework4 
# 赵维 2016211111班 学号2016210304

# file1 for creat 100 account
```
#!/bin/bash

resultd=0
resulta=a
a=(0 1 2 3 4 5 6 7 8 9)
b=(a b c d e f g h i j k l m n o p q r s t u v w x y z A B C D E F G H I J K L M N O P Q R S T U V W X Y Z)
result=0

echo "welcome home !" | tee /etc/motd

generateAlpha(){
	resulta=${b[$RANDOM % ${#a[@]}]}
}
generateDigit(){
	resultd=${a[$RANDOM % ${#a[@]}]}
}

rdmpassword(){
	generateDigit
	if [ $resultd -lt 5 ]
	then 	generateDigit
		result=$resultd
	else 	generateAlpha
		result=$resulta
	fi

	for i in 1 2 3 4 5 6 7
	do
		generateDigit
		if [ $resultd -lt 5 ]
		then	generateDigit
			result=$result$resultd
		else	generateAlpha
			result=$result$resulta
		fi
	done
}

creatAccount(){
	useradd -s /bin/bash stu$1
	echo stu$1:$2 | chpasswd
}
for j in $(seq -w 0 99) 
do
	rdmpassword
	creatAccount $j $result
	echo "stu$j:$result" | tee -a passwd.txt
done
```

# file2 for delete 100 account
```
#!/bin/bash 

for i in $(seq -w 0 99) 
do
    userdel stu$i 
done
rm passwd.txt
rm /etc/motd
```

# file passwd.txt -- all random password record
```
stu00:9g5fh0ai
stu01:0ff5e2hd
stu02:4e65bf5h
stu03:013a93de
stu04:864hacd2
stu05:c0224b97
stu06:1hcef4d9
stu07:eb2b3155
stu08:3efjdjei
stu09:efj4c8jd
stu10:jej2686e
stu11:f126fe8g
stu12:052ch7e1
stu13:4e5i92ag
stu14:77h8hj63
stu15:5454c366
stu16:4a43g2ea
stu17:ejcd9a10
stu18:9ha7a053
stu19:9aj0hg8g
stu20:ej3j13jj
stu21:92d91885
stu22:68b93efa
stu23:d2d7hd87
stu24:jae9509e
stu25:1g51a6i6
stu26:304ie13d
stu27:0e203g80
stu28:abgceg75
stu29:32bc75ee
stu30:71472h90
stu31:bd0ah160
stu32:4bbd3cgg
stu33:e2898gd3
stu34:a69hf7ai
stu35:e4j1e6bj
stu36:4bb9ehg4
stu37:c8629324
stu38:i2b57b7e
stu39:73dj11i8
stu40:ja2hjg45
stu41:9579gde7
stu42:c0834h5b
stu43:642a2h7g
stu44:fj7c89ca
stu45:88bbe5f9
stu46:9bb5d7aj
stu47:0bj08fca
stu48:jc043a2j
stu49:ii6i597b
stu50:4je5d6i8
stu51:60ch4143
stu52:8702i459
stu53:6160ach2
stu54:8h9748ef
stu55:169gicb3
stu56:52hj95j9
stu57:fcd5de99
stu58:j1ca4g59
stu59:4d7e4b5e
stu60:fd26a8fa
stu61:3fj6143g
stu62:ei5e7736
stu63:c235j3f0
stu64:4g1be2f8
stu65:9f9cb3j7
stu66:47731h7c
stu67:f8jbj74g
stu68:5e705b3g
stu69:0d8945af
stu70:ihc12geb
stu71:9hebchgg
stu72:di57gdc7
stu73:b3e68he8
stu74:6hgah4gj
stu75:465hbjb8
stu76:g331f08b
stu77:7b9jh1i7
stu78:9f791ded
stu79:h8c4addc
stu80:6gdf4g71
stu81:e2b6f7ji
stu82:chfc02b9
stu83:e7627ibe
stu84:i54eh0a6
stu85:7a76cg9f
stu86:1b8ab4i1
stu87:gb063c9a
stu88:8fc91308
stu89:66dj909g
stu90:ie2595ec
stu91:b95248d9
stu92:bg99ffj9
stu93:ihih5ge6
stu94:f1a21cbc
stu95:8bfa4065
stu96:647h3e89
stu97:e1jh2ga0
stu98:fecac7ba
stu99:9cece21e
```

# file4 user.txt -- all users when run file1
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
messagebus:x:106:110::/var/run/dbus:/bin/false
uuidd:x:107:111::/run/uuidd:/bin/false
lightdm:x:108:114:Light Display Manager:/var/lib/lightdm:/bin/false
whoopsie:x:109:116::/nonexistent:/bin/false
avahi-autoipd:x:110:119:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/bin/false
avahi:x:111:120:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
dnsmasq:x:112:65534:dnsmasq,,,:/var/lib/misc:/bin/false
colord:x:113:123:colord colour management daemon,,,:/var/lib/colord:/bin/false
speech-dispatcher:x:114:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/false
hplip:x:115:7:HPLIP system user,,,:/var/run/hplip:/bin/false
kernoops:x:116:65534:Kernel Oops Tracking Daemon,,,:/:/bin/false
pulse:x:117:124:PulseAudio daemon,,,:/var/run/pulse:/bin/false
rtkit:x:118:126:RealtimeKit,,,:/proc:/bin/false
saned:x:119:127::/var/lib/saned:/bin/false
usbmux:x:120:46:usbmux daemon,,,:/var/lib/usbmux:/bin/false
strongswan:x:121:65534::/var/lib/strongswan:/usr/sbin/nologin
postfix:x:122:129::/var/spool/postfix:/bin/false
vivizhao:x:1001:1001:ViviZhao,,,:/home/vivizhao:/bin/bash
stu00:x:1002:1002::/home/stu00:/bin/bash
stu01:x:1003:1003::/home/stu01:/bin/bash
stu02:x:1004:1004::/home/stu02:/bin/bash
stu03:x:1005:1005::/home/stu03:/bin/bash
stu04:x:1006:1006::/home/stu04:/bin/bash
stu05:x:1007:1007::/home/stu05:/bin/bash
stu06:x:1008:1008::/home/stu06:/bin/bash
stu07:x:1009:1009::/home/stu07:/bin/bash
stu08:x:1010:1010::/home/stu08:/bin/bash
stu09:x:1011:1011::/home/stu09:/bin/bash
stu10:x:1012:1012::/home/stu10:/bin/bash
stu11:x:1013:1013::/home/stu11:/bin/bash
stu12:x:1014:1014::/home/stu12:/bin/bash
stu13:x:1015:1015::/home/stu13:/bin/bash
stu14:x:1016:1016::/home/stu14:/bin/bash
stu15:x:1017:1017::/home/stu15:/bin/bash
stu16:x:1018:1018::/home/stu16:/bin/bash
stu17:x:1019:1019::/home/stu17:/bin/bash
stu18:x:1020:1020::/home/stu18:/bin/bash
stu19:x:1021:1021::/home/stu19:/bin/bash
stu20:x:1022:1022::/home/stu20:/bin/bash
stu21:x:1023:1023::/home/stu21:/bin/bash
stu22:x:1024:1024::/home/stu22:/bin/bash
stu23:x:1025:1025::/home/stu23:/bin/bash
stu24:x:1026:1026::/home/stu24:/bin/bash
stu25:x:1027:1027::/home/stu25:/bin/bash
stu26:x:1028:1028::/home/stu26:/bin/bash
stu27:x:1029:1029::/home/stu27:/bin/bash
stu28:x:1030:1030::/home/stu28:/bin/bash
stu29:x:1031:1031::/home/stu29:/bin/bash
stu30:x:1032:1032::/home/stu30:/bin/bash
stu31:x:1033:1033::/home/stu31:/bin/bash
stu32:x:1034:1034::/home/stu32:/bin/bash
stu33:x:1035:1035::/home/stu33:/bin/bash
stu34:x:1036:1036::/home/stu34:/bin/bash
stu35:x:1037:1037::/home/stu35:/bin/bash
stu36:x:1038:1038::/home/stu36:/bin/bash
stu37:x:1039:1039::/home/stu37:/bin/bash
stu38:x:1040:1040::/home/stu38:/bin/bash
stu39:x:1041:1041::/home/stu39:/bin/bash
stu40:x:1042:1042::/home/stu40:/bin/bash
stu41:x:1043:1043::/home/stu41:/bin/bash
stu42:x:1044:1044::/home/stu42:/bin/bash
stu43:x:1045:1045::/home/stu43:/bin/bash
stu44:x:1046:1046::/home/stu44:/bin/bash
stu45:x:1047:1047::/home/stu45:/bin/bash
stu46:x:1048:1048::/home/stu46:/bin/bash
stu47:x:1049:1049::/home/stu47:/bin/bash
stu48:x:1050:1050::/home/stu48:/bin/bash
stu49:x:1051:1051::/home/stu49:/bin/bash
stu50:x:1052:1052::/home/stu50:/bin/bash
stu51:x:1053:1053::/home/stu51:/bin/bash
stu52:x:1054:1054::/home/stu52:/bin/bash
stu53:x:1055:1055::/home/stu53:/bin/bash
stu54:x:1056:1056::/home/stu54:/bin/bash
stu55:x:1057:1057::/home/stu55:/bin/bash
stu56:x:1058:1058::/home/stu56:/bin/bash
stu57:x:1059:1059::/home/stu57:/bin/bash
stu58:x:1060:1060::/home/stu58:/bin/bash
stu59:x:1061:1061::/home/stu59:/bin/bash
stu60:x:1062:1062::/home/stu60:/bin/bash
stu61:x:1063:1063::/home/stu61:/bin/bash
stu62:x:1064:1064::/home/stu62:/bin/bash
stu63:x:1065:1065::/home/stu63:/bin/bash
stu64:x:1066:1066::/home/stu64:/bin/bash
stu65:x:1067:1067::/home/stu65:/bin/bash
stu66:x:1068:1068::/home/stu66:/bin/bash
stu67:x:1069:1069::/home/stu67:/bin/bash
stu68:x:1070:1070::/home/stu68:/bin/bash
stu69:x:1071:1071::/home/stu69:/bin/bash
stu70:x:1072:1072::/home/stu70:/bin/bash
stu71:x:1073:1073::/home/stu71:/bin/bash
stu72:x:1074:1074::/home/stu72:/bin/bash
stu73:x:1075:1075::/home/stu73:/bin/bash
stu74:x:1076:1076::/home/stu74:/bin/bash
stu75:x:1077:1077::/home/stu75:/bin/bash
stu76:x:1078:1078::/home/stu76:/bin/bash
stu77:x:1079:1079::/home/stu77:/bin/bash
stu78:x:1080:1080::/home/stu78:/bin/bash
stu79:x:1081:1081::/home/stu79:/bin/bash
stu80:x:1082:1082::/home/stu80:/bin/bash
stu81:x:1083:1083::/home/stu81:/bin/bash
stu82:x:1084:1084::/home/stu82:/bin/bash
stu83:x:1085:1085::/home/stu83:/bin/bash
stu84:x:1086:1086::/home/stu84:/bin/bash
stu85:x:1087:1087::/home/stu85:/bin/bash
stu86:x:1088:1088::/home/stu86:/bin/bash
stu87:x:1089:1089::/home/stu87:/bin/bash
stu88:x:1090:1090::/home/stu88:/bin/bash
stu89:x:1091:1091::/home/stu89:/bin/bash
stu90:x:1092:1092::/home/stu90:/bin/bash
stu91:x:1093:1093::/home/stu91:/bin/bash
stu92:x:1094:1094::/home/stu92:/bin/bash
stu93:x:1095:1095::/home/stu93:/bin/bash
stu94:x:1096:1096::/home/stu94:/bin/bash
stu95:x:1097:1097::/home/stu95:/bin/bash
stu96:x:1098:1098::/home/stu96:/bin/bash
stu97:x:1099:1099::/home/stu97:/bin/bash
stu98:x:1100:1100::/home/stu98:/bin/bash
stu99:x:1101:1101::/home/stu99:/bin/bash
```


