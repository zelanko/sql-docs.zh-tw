---
title: Microsoft Drivers for PHP for SQL Server 的 Linux 和 macOS 安裝教學課程 | Microsoft Docs
ms.date: 05/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: 2e1e6e6773644b12b6259349c522113ec66a0d43
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65502771"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的 Linux 和 macOS 安裝教學課程
下列指示假設一個全新的環境，並示範如何在 Ubuntu 16.04、18.04 及 18.10；RedHat 7；Debian 8 和 9；Suse 12 和 15，以及 macOS 10.12、10.13 及 10.14 上安裝 PHP 7.x、Microsoft ODBC 驅動程式、Apache 及 Microsoft Drivers for PHP for SQL Server。 這些指示建議使用 PECL 安裝驅動程式，但您也可以從 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) \(英文\) Github 專案頁面中下載預先建置的二進位檔，並遵循[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 中的指示進行安裝。 如需載入延伸模組以及我們未將延伸模組新增至 php.ini 的原因說明，請參閱關於[載入驅動程式](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)的小節。

這些指示預設會安裝 PHP 7.3。 請注意，部分支援的 Linux 散發版本會預設為 PHP 7.0 或更早版本，但適用於 SQL Server 的 PHP 驅動程式不支援這些版本，請參閱每節開頭的注意事項以改為安裝 PHP 7.1 或 7.2。

## <a name="contents-of-this-page"></a>此頁面的內容：

- [在 Ubuntu 16.04、18.04 和 18.10 上安裝驅動程式](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [在 Red Hat 7 上安裝驅動程式](#installing-the-drivers-on-red-hat-7)
- [在 Debian 8 和 9 上安裝驅動程式](#installing-the-drivers-on-debian-8-and-9)
- [在 Suse 12 和 15 上安裝驅動程式](#installing-the-drivers-on-suse-12-and-15)
- [在 macOS Sierra、High Sierra 和 Mojave 上安裝驅動程式](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>在 Ubuntu 16.04、18.04 和 18.10 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.1 或 7.2，在下列命令中使用 7.1 或 7.2 來取代 7.3。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 和 macOS 安裝頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上的指示來安裝適用於 Ubuntu 的 ODBC 驅動程式。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 並測試範例指令碼
```
sudo service apache2 restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-red-hat-7"></a>在 Red Hat 7 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.1 或 7.2，在下列命令中分別使用 remi-php71 或 remi-php72 來取代 remi-php73。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 和 macOS 安裝頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上的指示來安裝適用於 Red Hat 7 的 ODBC 驅動程式。

使用含 PHP 7.2 或 7.3 的 PECL 來編譯 PHP 驅動程式，需要比預設值還新的 GCC：
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
即使您已升級 GCC，PECL 中的問題可能還是會阻止正確安裝最新版的驅動程式。 若要安裝、下載套件並以手動方式編譯 (類似 pdo_sqlsrv 的步驟)：
```
pecl download sqlsrv
tar xvzf sqlsrv-5.6.1.tgz
cd sqlsrv-5.6.1/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
或者，您可以從 [Github 專案頁面](https://github.com/Microsoft/msphpsql/releases) \(英文\) 下載預先建置的二進位檔，或從 Remi 存放庫安裝：
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>步驟 4： 安裝 Apache
```
sudo yum install httpd
```
預設會安裝 SELinux，並以強制模式執行。 若要允許 Apache 透過 SELinux 連線到資料庫，請執行下列命令：
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 並測試範例指令碼
```
sudo apachectl restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>在 Debian 8 和 9 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.1 或 7.2，在下列命令中使用 7.1 或 7.2 來取代 7.3。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 和 macOS 安裝頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上的指示來安裝適用於 Debian 的 ODBC 驅動程式。 

此外，您可能也需要產生正確的地區設定，以取得要在瀏覽器中正確顯示的 PHP 輸出。 例如，針對 en_US UTF-8 地區設定，執行下列命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 並測試範例指令碼
```
sudo service apache2 restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-suse-12-and-15"></a>在 Suse 12 和 15 上安裝驅動程式

> [!NOTE]
> 在下列指示中，使用您的 Suse 版本來取代 <SuseVersion>；如果您要使用 Suse Enterprise Linux 15，則其將是 SLE_15 或 SLE_15_SP1，對於其他版本也是如此。 並非所有 PHP 版本都可供適用於 Suse Linux 的所有版本使用，請參閱 `http://download.opensuse.org/repositories/devel:/languages:/php` 以查看哪些版本的 Suse 具有可用的預設版本 PHP，或 `http://download.opensuse.org/repositories/devel:/languages:/php:/` 以查看哪些其他版本的 PHP 可供哪些版本的 Suse 使用。

> [!NOTE]
> 適用於 PHP 7.3 的套件不適用 Suse 12。 若要安裝 PHP 7.1，使用下列 URL 來取代以下的存放庫 URL：`https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`。
> 若要安裝 PHP 7.2，使用下列 URL 來取代以下的存放庫 URL：`https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 和 macOS 安裝頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上的指示來安裝適用於 Suse 的 ODBC 驅動程式。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
> [!NOTE]
> 如果您收到錯誤訊息，指出 `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`，請編輯 /usr/bin/pecl 上的 pecl 指令碼，並移除最後一行中的 `-n` 參數。 此參數可防止 PECL 在呼叫 PHP 時載入 ini 檔案，這可避免載入 OpenSSL 延伸模組。

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 並測試範例指令碼
```
sudo systemctl restart apache2
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>在 macOS Sierra、High Sierra 和 Mojave 上安裝驅動程式

如果您尚未安裝，請以如下方式安裝 brew：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安裝 PHP 7.1 或 7.2，在下列命令中分別使用 php@7.1 或 php@7.2 來取代 php@7.3。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP 現在應該位於您的路徑中：執行 `php -v` 以確認您正在執行正確的 PHP 版本。 如果 PHP 不在您的路徑中或不是正確版本，請執行下列命令：
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 和 macOS 安裝頁面](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上的指示來安裝適用於 macOS 的 ODBC 驅動程式。 

此外，您可能需要安裝 GNU 製作工具：
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
brew install apache2
```
若要尋找 Apache 設定檔以進行 Apache 安裝，請執行 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
同時，在下列命令中取代 `httpd.conf` 的路徑：
```
echo "LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5： 重新啟動 Apache 並測試範例指令碼
```
sudo apachectl restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="testing-your-installation"></a>測試您的安裝

若要測試此範例指令碼，在系統的文件根目錄中建立名為 testsql.php 的檔案。 這在 Ubuntu、Debian 和 Redhat 上為 `/var/www/html/`、在 SUSE 上為 `/srv/www/htdocs`，或者在 macOS 上為 `/usr/local/var/www`。 將下列指令碼複製到其中，適當地取代伺服器、資料庫、使用者名稱和密碼。
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
將您的瀏覽器指向 https://localhost/testsql.php (macOS 上的 https://localhost:8080/testsql.php)。 您現在應該能夠連線到您的 SQL Server/Azure SQL 資料庫。

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
