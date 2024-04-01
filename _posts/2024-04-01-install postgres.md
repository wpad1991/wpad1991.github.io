

### 0 - 들어가면서
***
Open Source DB에 대한 수요가 늘어나면서 Postgres를 많이 사용한다는 이야기를 들었다.
그래서 Postgres를 설치하는 방법을 정리해두려고 한다.
아키텍처와 관련된 내용은 별도로 다루기로 하고, 이 페이지에서는 설치 관련된 내용만 다루도록 한다.

### 1 - 설치
***

수행되는 서버의 환경을 확인한다.
centos이후 버전인 rocky를 사용하여 환경에서 수행하였다.
'''
[root@localhost ~]# cat /etc/*release
NAME="Rocky Linux"
VERSION="9.3 (Blue Onyx)"
ID="rocky"
ID_LIKE="rhel centos fedora"
VERSION_ID="9.3"
PLATFORM_ID="platform:el9"
PRETTY_NAME="Rocky Linux 9.3 (Blue Onyx)"
ANSI_COLOR="0;32"
LOGO="fedora-logo-icon"
CPE_NAME="cpe:/o:rocky:rocky:9::baseos"
HOME_URL="https://rockylinux.org/"
BUG_REPORT_URL="https://bugs.rockylinux.org/"
SUPPORT_END="2032-05-31"
ROCKY_SUPPORT_PRODUCT="Rocky-Linux-9"
ROCKY_SUPPORT_PRODUCT_VERSION="9.3"
REDHAT_SUPPORT_PRODUCT="Rocky Linux"
REDHAT_SUPPORT_PRODUCT_VERSION="9.3"
Rocky Linux release 9.3 (Blue Onyx)
Rocky Linux release 9.3 (Blue Onyx)
Rocky Linux release 9.3 (Blue Onyx)
'''


테스트를 하기 위해 별도의 계정을 생성해준다.
테스트를 하기 위한 제일 좋은 방법은 별도의 독립된 가상 환경을 이용하는 방법이지만, 환경을 구축할 수 없는 상황이라 유저만 별도로 생성하여 작업한다.
특정 서비스를 수행할 때는 root가 아닌 전용 유저를 사용하는 것이 좋다. 이유는 프로세스를 확인하기 쉽기 때문이다.

'''
# postgres1 유저를 생성한다.
[root@localhost ~]# useradd postgres1
[root@localhost ~]# passwd postgres1
Changing password for user postgres1.
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: all authentication tokens updated successfully.
[root@localhost ~]# su - postgres1
'''

<img src="../assets/images/20240401_postgres_install_1.png" style="width:200p"/> 
설치 방법은 공식 홈페이지를 참조한다. 공식 문서에서 설치하고자 하는 버전과 플랫폼을 선택하고 아키텍처를 선택하고 스크립트 따라 설치한다.
https://www.postgresql.org/download/linux/redhat/

'''
# Install the repository RPM:
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# Disable the built-in PostgreSQL module:
sudo dnf -qy module disable postgresql

# Install PostgreSQL:
sudo dnf install -y postgresql16-server

# Optionally initialize the database and enable automatic start:
sudo /usr/pgsql-16/bin/postgresql-16-setup initdb
sudo systemctl enable postgresql-16
sudo systemctl start postgresql-16
'''

