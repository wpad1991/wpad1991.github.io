



'''
C:\Users\jskim>wsl --list --online
다음은 설치할 수 있는 유효한 배포판 목록입니다.
'wsl.exe --install <Distro>'를 사용하여 설치합니다.

NAME                                   FRIENDLY NAME
Ubuntu                                 Ubuntu
Debian                                 Debian GNU/Linux
kali-linux                             Kali Linux Rolling
Ubuntu-18.04                           Ubuntu 18.04 LTS
Ubuntu-20.04                           Ubuntu 20.04 LTS
Ubuntu-22.04                           Ubuntu 22.04 LTS
OracleLinux_7_9                        Oracle Linux 7.9
OracleLinux_8_7                        Oracle Linux 8.7
OracleLinux_9_1                        Oracle Linux 9.1
openSUSE-Leap-15.5                     openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4    SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5           SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed                    openSUSE Tumbleweed

'''


'''
C:\Users\jskim>wsl --install OracleLinux_8_7
설치 중: Oracle Linux 8.7
Oracle Linux 8.7이(가) 설치되었습니다.
Oracle Linux 8.7을(를) 시작하는 중...
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: jskim
Changing password for user jskim.
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: all authentication tokens updated successfully.
Installation successful!
'''

'''
C:\Users\jskim>wsl --list
Linux용 Windows 하위 시스템 배포:
OracleLinux_8_7(기본값)
'''

'''
C:\Users\jskim>wsl --version
WSL 버전: 2.1.5.0
커널 버전: 5.15.146.1-2
WSLg 버전: 1.0.60
MSRDC 버전: 1.2.5105
Direct3D 버전: 1.611.1-81528511
DXCore 버전: 10.0.25131.1002-220531-1700.rs-onecore-base2-hyp
Windows 버전: 10.0.22631.3296
'''