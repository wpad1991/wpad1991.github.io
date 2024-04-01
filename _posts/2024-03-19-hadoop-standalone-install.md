


처음으로 포스트하는 기술적인 내용의 정리 사항으로는 hadoop을 standalone으로 구성하는 방법에 대해 쓰려고한다.
hadoop은 보통 여러 서버를 이용해서 Cluster로 구성하여 사용하는 경우가 많은데, 이 때 네트워크 설정 관련 내용이 들어가게 되는데 linux의 설정 관련된 부분에 대해 이야기할 내용이 많아 처음에는 간단하게 시작해보려고 한다.


0 - 개요
***

데이터 가상화 솔루션을 하면서 외부 업체의 ODBC Tools을 사용하게 되었다. 사용하면서 문제는 해당 ODBC Tools에서는 Request 관리가 안된다는 것이다.
기본적으로 하나의 탭에서 쿼리를 수행하고 닫으면 해당 탭에서 사용한 Request는 닫힐거라고 예상되지만, 해당 요청의 Cursor는 모든 데이터를 Fetch하지 않았기 때문에 Request가 남아있는 상태이다.
그리고 해당 Request는 탭을 닫아버렸기 때문에 종료할 수 없다. 이 문제는 데이터 가상화를 사용하면서 확인한 문제였고, 이 ODBC Tools은 이미 상용에서 문제없이 사용하고 있기 때문에 일종의 검증이 필요하게 되었다.
ODBC Tools의 문제인지 데이터 가상화의 문제인지를 확인하기 위해 다른 DB를 연결했을 때 이 ODBC Tools은 어떻게 동작하는 지 확인이 필요하게 되었다. 따라서 hadoop-hive 환경을 구성이 필요하게 되었다.

hadoop과 hive를 개별로 설치하려고 하였지만, 찾아보니 ambari를 많이 이용하는 것 같고 실제로 프로젝트에서도 ambari를 이용해 환경이 구성되어 있기 때문에 ambari로 환경을 구성하려고 시도하였다.
문제는 내가 원하는 버전의 ambari 버전을 이용해서 설치를 1차 시도했지만, 실패하였다. 기본적으로 사용할 수 있는 Repository가 404 Not Found를 발생하여서 사용할 수가 없게 되었다.
그래서 외부의 Repository가 아니라, 각 설치 파일을 개별로 구해서 File Repository를 구성하여 수행하려고 시도하였다.
원래 설치하려던 버전은 HDP 3.1 버전인데, x86 arch 버전의 설치 파일을 찾기가 힘들었지만 중국 미러 서버에서 내가 사용하려는 버전을 찾을 수 있어서 사용하였다.
몇 차례 시도하다가 ambari를 2.7.3 버전에서 2.7.8버전으로 다시 설치하여 사용해보려고 시도하였다. (2.6.2, 2.7.5 버전은 시도하다가 실패하였다.)
결국 이리 저리 헤매다가 ambari와 bigtop을 포기하고 각 hadoop과 hive를 별도로 설치하기로 하였다.
이 부분에 대한 시행 착오와 Trouble Shooting에 대한 부분은 이야기할 수 있는 날이 있으면 좋겠다.

1 - 환경 확인
***
설치를 진행하기에 앞서 환경 적인 부분에 대한 확인을 수행하였다.

```
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
```

