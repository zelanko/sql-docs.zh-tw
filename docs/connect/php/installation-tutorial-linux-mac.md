---
title: Linux 和 macOS 的 Microsoft Drivers for PHP for SQL Server 的安裝教學課程 |Microsoft Docs
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: af05ede442133465e7f268665bac4cd11a17f653
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604598"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux 和 macOS 的 Microsoft Drivers for PHP for SQL Server 的安裝教學課程
下列指示假設全新的環境，並示範如何在 Ubuntu 16.04、 17.10 和 18.04，RedHat 7、 Debian 8 和 9，Suse 12 和 macOS 10.11 上的 SQL Server 安裝 PHP 7.x、 Microsoft ODBC 驅動程式、 Apache 和 Microsoft Drivers for PHP10.12 和 10.13。 這些指示通知使用安裝驅動程式 PECL，但您也可以下載預先建置的二進位檔，從[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 專案頁面，並遵循中的指示進行安裝[載入 Microsoft Drivers for PHP，適用於 SQL Server](../../connect/php/loading-the-php-sql-driver.md)。 延伸模組的載入和為什麼我們不會將延伸模組加入 php.ini 的說明，請參閱上一節[載入的驅動程式](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)。

這些指示安裝 PHP 7.2 的預設值--請參閱每個區段，來安裝 PHP 7.0 或 7.1 開頭的附註。

## <a name="contents-of-this-page"></a>此頁面的內容：

- [在 Ubuntu 16.04、 17.10 和 18.04 上安裝驅動程式](#installing-the-drivers-on-ubuntu-1604-1710-and-1804)
- [在 Red Hat 7 上安裝驅動程式](#installing-the-drivers-on-red-hat-7)
- [在 Debian 8 和 9 上安裝的驅動程式](#installing-the-drivers-on-debian-8-and-9)
- [在 Suse 12 上安裝的驅動程式](#installing-the-drivers-on-suse-12)
- [El Capitan、 Sierra 和 High Sierra 在 macOS 上安裝的驅動程式](#installing-the-drivers-on-macos-el-capitan-sierra-and-high-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-1710-and-1804"></a>在 Ubuntu 16.04，17.10 和 18.04 上安裝的驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代 7.2 7.0 或 7.1 中的下列命令。
> 如 Ubuntu 18.04 新增 ondrej 存放庫的步驟不需要，除非需要 PHP 7.0 或 7.1。 不過，在 Ubuntu 18.04 安裝 PHP 7.0 或 7.1 可能不如 ondrej 存放庫中的套件會隨附可能與基底安裝 Ubuntu 18.04 衝突的相依性。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循上的指示安裝 ODBC 驅動程式適用於 Ubuntu [Linux 和 macOS 的 [安裝] 頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache，並測試的範例指令碼
```
sudo service apache2 restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-red-hat-7"></a>在 Red Hat 7 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代 remi php72 remi php70 或 remi-php71 分別在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循上的指示安裝 ODBC 驅動程式的 Red Hat 7 [Linux 和 macOS 的 [安裝] 頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

編譯與 PECL 與 PHP 7.2 的 PHP 驅動程式需要較新的 GCC 與預設值：
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
即使您已升級 GCC PECL 的問題可能會導致驅動程式的最新版本的正確安裝。 若要安裝、 下載的套件及編譯以手動方式 （如 pdo_sqlsrv 類似的步驟）：
```
pecl download sqlsrv
tar xvzf sqlsrv-5.3.0.tgz
cd sqlsrv-5.3.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
或者，您可以下載預先建置的二進位檔，從[Github 專案頁面](https://github.com/Microsoft/msphpsql/releases)，或從 Remi 存放庫安裝：
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>步驟 4： 安裝 Apache
```
sudo yum install httpd
```
SELinux 預設會安裝，並以強制模式執行。 若要允許連接到資料庫 SELinux 透過 Apache，請執行下列命令：
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache，並測試的範例指令碼
```
sudo apachectl restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>在 Debian 8 和 9 上安裝的驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代在下列命令中的 7.2 7.0 或 7.1。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循上的指示安裝 ODBC 驅動程式的 Debian [Linux 和 macOS 的 [安裝] 頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

此外，您可能也需要產生正確的地區設定，以取得正確顯示瀏覽器中的 PHP 輸出。 比方說，如果 en_US utf-8 地區設定中，執行下列命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache，並測試的範例指令碼
```
sudo service apache2 restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-suse-12"></a>在 Suse 12 上安裝的驅動程式

> [!NOTE]
> 若要安裝 PHP 7.0，請略過下列命令新增儲存機制-7.0 是預設的 PHP 上 suse 12。
> 若要安裝 PHP 7.1，請將以下的存放庫 URL 取代下列 URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循上的指示安裝 ODBC 驅動程式的 Suse 12 [Linux 和 macOS 的 [安裝] 頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定驅動程式載入
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache，並測試的範例指令碼
```
sudo systemctl restart apache2
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="installing-the-drivers-on-macos-el-capitan-sierra-and-high-sierra"></a>El Capitan、 Sierra 和 High Sierra 在 macOS 上安裝的驅動程式

如果您還沒有它，安裝 brew 如下所示：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安裝 PHP 7.0 或 7.1，取代php@7.2具有php@7.0或php@7.1分別在下列命令。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP 現在應該位於您的路徑--執行`php -v`確認您正在執行正確的 PHP 版本。 如果 PHP 不在您的路徑，或不正確的版本，執行下列命令：
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循上的指示來安裝 ODBC driver for macOS [Linux 和 macOS 的 [安裝] 頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

此外，您可能需要安裝 GNU 製作工具：
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 和設定驅動程式載入
```
brew install apache2
```
若要尋找 Apache Apache 安裝組態檔，請執行 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
使用路徑來取代和`httpd.conf`在下列命令：
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache，並測試的範例指令碼
```
sudo apachectl restart
```
若要測試您的安裝，請參閱[測試安裝](#testing-your-installation)這份文件的結尾。

## <a name="testing-your-installation"></a>測試您的安裝

若要測試此範例指令碼，建立名為 testsql.php 系統的文件根目錄中的檔案。 這是`/var/www/html/`在 Ubuntu、 Debian 和 Redhat`/srv/www/htdocs`在 SUSE 上或`/usr/local/var/www`在 macOS 上。 複製下列指令碼，取代伺服器、 資料庫、 使用者名稱和適當的密碼。
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
您的瀏覽器指向 https://localhost/testsql.php(https://localhost:8080/testsql.php在 macOS 上)。 您現在應該能夠連線到您的 SQL Server/Azure SQL database。

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
