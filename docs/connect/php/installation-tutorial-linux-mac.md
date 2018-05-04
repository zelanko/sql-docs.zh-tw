---
title: Linux 及 macOS Microsoft Drivers for PHP for SQL Server 安裝教學課程 |Microsoft 文件
ms.date: 04/11/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: c9a28604fb55c81c4fcca0df542110d6347f3ee5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux 及 macOS Microsoft Drivers for PHP for SQL Server 安裝教學課程
下列指示假設乾淨的環境，並示範如何安裝 PHP 7.x、 Microsoft ODBC 驅動程式、 Apache 和 Microsoft Drivers for PHP for Ubuntu 16.04 和 17.10，RedHat 7 上的 SQL Server、 Debian 8 和 9、 Suse 12 及 macOS X 10.11 和 10.12。 這些指示建議安裝的驅動程式使用 PECL，但您也可以下載預先建置的二進位檔案從[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 頁面的專案，並將其中的指示安裝[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。 載入擴充功能，以及為什麼我們不會將擴充功能加入 php.ini 的說明，請參閱上節[載入驅動程式](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)。

依預設-這些指示安裝 PHP 7.2 參閱每個區段，以安裝 PHP 7.0 或 7.1 開頭的資訊。

## <a name="contents-of-this-page"></a>此頁面的內容：

- [在 Ubuntu 16.04 和 17.10 上安裝的驅動程式](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [Red Hat 7 上安裝驅動程式](#installing-the-drivers-on-red-hat-7)
- [在 Debian 8 和 9 中安裝的驅動程式](#installing-the-drivers-on-debian-8-and-9)
- [Suse 12 上安裝驅動程式](#installing-the-drivers-on-suse-12)
- [El Capitan 和利也 macOS 上安裝驅動程式](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>在 Ubuntu 16.04 和 17.10 上安裝的驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代 7.2 7.0 或 7.1 在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
Ubuntu 的安裝 ODBC 驅動程式的指示[Linux 及 macOS 安裝 頁面上](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： Microsoft SQL server 安裝的 PHP 驅動程式
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定 載入驅動程式
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 和測試的範例指令碼
```
sudo service apache2 restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-red-hat-7"></a>Red Hat 7 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代 remi php72 remi php70 或 remi-php71 分別在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
Red Hat 7 安裝 ODBC 驅動程式的指示[Linux 及 macOS 安裝 頁面上](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

編譯與 PECL 與 PHP 7.2 的 PHP 驅動程式需要較新的 GCC 比預設值：
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： Microsoft SQL server 安裝的 PHP 驅動程式
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
即使您已升級 GCC PECL 的問題可能會阻礙正常安裝最新版本的驅動程式。 若要安裝、 下載的套件，並手動編譯：
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
或者，您可以下載預先建置的二進位檔案從[Github 專案頁面](https://github.com/Microsoft/msphpsql/releases)，或是安裝來自 Remi 儲存機制：
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>步驟 4： 安裝 Apache
```
sudo yum install httpd
```
SELinux 預設會安裝，並強制模式中執行。 若要讓連線到資料庫 SELinux 透過 Apache，執行下列命令：
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 和測試的範例指令碼
```
sudo apachectl restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>在 Debian 8 和 9 中安裝的驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代 7.0 或 7.1 7.2 在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
安裝 ODBC 驅動程式遵循指示 Debian [Linux 及 macOS 安裝 頁面上](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

您也可能需要產生正確的地區設定，以取得正確顯示瀏覽器中的 PHP 輸出。 En_US utf-8 地區設定，例如，執行下列命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： Microsoft SQL server 安裝的 PHP 驅動程式
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定 載入驅動程式
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 和測試的範例指令碼
```
sudo service apache2 restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-suse-12"></a>Suse 12 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0，略過下面的命令加入儲存機制-7.0 是預設的 PHP suse 12 上。
> 若要安裝 PHP 7.1，下方的儲存機制 URL 取代為下列 URL: `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
安裝 ODBC 驅動程式遵循指示 Suse 12 [Linux 及 macOS 安裝 頁面上](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： Microsoft SQL server 安裝的 PHP 驅動程式
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定 載入驅動程式
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 和測試的範例指令碼
```
sudo systemctl restart apache2
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>El Capitan 和利也 macOS 上安裝驅動程式

如果您還沒有它，安裝 brew，如下所示：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代php@7.2與php@7.0或php@7.1分別在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP 現在應該在您的路徑--執行`php -v`確認您正在執行 PHP 的正確版本。 如果 PHP 不在您的路徑，或不正確的版本，執行下列命令：
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循指示安裝 ODBC driver for macOS [Linux 及 macOS 安裝 頁面上](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

此外，您可能需要安裝 GNU 產生工具：
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： Microsoft SQL server 安裝的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定 載入驅動程式
```
brew install apache2
```
若要尋找 Apache Apache 安裝組態檔，請執行 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
和路徑來取代`httpd.conf`在下列命令：
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 和測試的範例指令碼
```
sudo apachectl restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="testing-your-installation"></a>測試您的安裝

若要測試這個範例指令碼，建立稱為 testsql.php 系統的文件根目錄中的檔案。 這是`/var/www/html/`Ubuntu、 Debian，及 Redhat，`/srv/www/htdocs`上 SUSE，或`/usr/local/var/www`macOS 上。 複製下列指令碼，取代伺服器、 資料庫、 使用者名稱和適當的密碼。
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
指向您的瀏覽器http://localhost/testsql.php(http://localhost:8080/testsql.php macOS 上)。 您現在應該能夠連線到您的 SQL Server/Azure SQL database。

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[系統需求的 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
