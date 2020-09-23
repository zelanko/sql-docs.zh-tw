---
title: Drivers for PHP 的 Linux 和 macOS 安裝
description: 在這些指示中，您將了解如何在 Linux 或 macOS 上安裝 Microsoft Drivers for PHP for SQL Server。
ms.date: 04/15/2020
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
manager: v-mabarw
ms.openlocfilehash: ee4938e8a0d226f668fabf3aaf4db1359ab6bf61
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807014"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的 Linux 和 macOS 安裝教學課程
下列指示假設一個全新的環境，並示範如何在 Ubuntu 16.04、18.04 及 20.04；RedHat 7 和 8；Debian 8、9 和 10；Suse 12 和 15；Alpine 3.11，以及 macOS 10.13、10.14 及 10.15 上安裝 PHP 7.x、Microsoft ODBC 驅動程式、Apache Web 伺服器，以及 Microsoft Drivers for PHP for SQL Server。 這些指示建議使用 PECL 安裝驅動程式，但您也可以從 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) \(英文\) GitHub 專案頁面中下載預先建置的二進位檔，並遵循[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 中的指示進行安裝。 如需載入延伸模組以及我們未將延伸模組新增至 php.ini 的原因說明，請參閱關於[載入驅動程式](../../connect/php/loading-the-php-sql-driver.md#loading-the-driver-at-php-startup)的小節。

這些指示預設會使用 `pecl install` 安裝 PHP 7.4。 您可能需要先執行 `pecl channel-update pecl.php.net`。 請注意，部分支援的 Linux 發行版本會預設為 PHP 7.1 或更早版本，但最新版本的 PHP drivers for SQL Server 並不支援這些版本。請參閱每節開頭的注意事項以改為安裝 PHP 7.2 或 7.3。

同時包含在 Ubuntu 上安裝 PHP FastCGI Process Manager (PHP-FPM) 的指示。 如果使用 nginx Web 伺服器而非 Apache，便會需要此項目。

## <a name="contents-of-this-page"></a>此頁面的內容

- [在 Ubuntu 16.04、18.04 和 20.04 上安裝驅動程式](#installing-the-drivers-on-ubuntu-1604-1804-and-2004)
- [在 Ubuntu 上搭配 PHP-FPM 安裝驅動程式](#installing-the-drivers-with-php-fpm-on-ubuntu)
- [在 Red Hat 7 和 8 上安裝驅動程式](#installing-the-drivers-on-red-hat-7-and-8)
- [在 Debian 8、9 和 10 上安裝驅動程式](#installing-the-drivers-on-debian-8-9-and-10)
- [在 Suse 12 和 15 上安裝驅動程式](#installing-the-drivers-on-suse-12-and-15)
- [在 Alpine 3.11 上安裝驅動程式](#installing-the-drivers-on-alpine-311)
- [在 macOS High Sierra、Mojave 和 Catalina 上安裝驅動程式](#installing-the-drivers-on-macos-high-sierra-mojave-and-catalina)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-2004"></a>在 Ubuntu 16.04、18.04 和 20.04 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中使用 7.2 或 7.3 來取代 7.4。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Ubuntu 的 ODBC 驅動程式。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

如果系統中只有單一 PHP 版本，則最後的步驟可以簡化為 `phpenmod sqlsrv pdo_sqlsrv`。

### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo service apache2 restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-with-php-fpm-on-ubuntu"></a>在 Ubuntu 上搭配 PHP-FPM 安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中使用 7.2 或 7.3 來取代 7.4。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml php7.4-fpm -y --allow-unauthenticated
```
透過執行下列內容來確認 PHP-FPM 服務的狀態
```
systemctl status php7.4-fpm
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Ubuntu 的 ODBC 驅動程式。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl config-set php_ini /etc/php/7.4/fpm/php.ini
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```
如果系統中只有單一 PHP 版本，則最後的步驟可以簡化為 `phpenmod sqlsrv pdo_sqlsrv`。

確認 `sqlsrv.ini` 與 `pdo_sqlsrv.ini` 皆位於 `/etc/php/7.4/fpm/conf.d/` 中：
```
ls /etc/php/7.4/fpm/conf.d/*sqlsrv.ini
```
重新啟動 PHP-FPM 服務：
```
sudo systemctl restart php7.4-fpm
```

### <a name="step-4-install-and-configure-nginx"></a>步驟 4： 安裝及設定 nginx
```
sudo apt-get update
sudo apt-get install nginx
sudo systemctl status nginx
```
若要設定 nginx，您必須編輯 `/etc/nginx/sites-available/default` 檔案。 將 `index.php` 新增至下列清單中顯示 `# Add index.php to the list if you are using PHP` 的區段：
```
# Add index.php to the list if you are using PHP
index index.html index.htm index.nginx-debian.html index.php;
```
接下來，請以如下方式修改 `# pass PHP scripts to FastCGI server` 後面的區段：
```
# pass PHP scripts to FastCGI server
#
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
}
```
### <a name="step-5-restart-nginx-and-test-the-sample-script"></a>步驟 5。 重新啟動 nginx 並測試範例指令碼
```
sudo systemctl restart nginx.service
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-red-hat-7-and-8"></a>在 Red Hat 7 和 8 上安裝驅動程式

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

若要在 Red Hat 7 上安裝 PHP，請執行下列內容：
> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中分別使用 remi-php72 或 remi-php73 來取代 remi-php74。
```
sudo su
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php74
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```

若要在 Red Hat 8 上安裝 PHP，請執行下列內容：
> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中分別使用 remi-7.2 或 remi-7.3 來取代 remi-7.4。
```
sudo su
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf install yum-utils
dnf module reset php
dnf module install php:remi-7.4
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
dnf update
dnf install php-pdo php-pear php-devel
```

### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Red Hat 7 或 8 的 ODBC 驅動程式。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```

或者，您也可以從 Remi 存放庫安裝：
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
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo apachectl restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-debian-8-9-and-10"></a>在 Debian 8、9 和 10 上安裝驅動程式

> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中使用 7.2 或 7.3 來取代 7.4。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.4 php7.4-dev php7.4-xml php7.4-intl
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Debian 的 ODBC 驅動程式。 

此外，您可能也需要產生正確的地區設定，以取得要在瀏覽器中正確顯示的 PHP 輸出。 例如，針對 en_US UTF-8 地區設定，執行下列命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```
您可能需要將 `/usr/sbin` 新增到您的 `$PATH`，因為 `locale-gen` 可執行檔位於這裡。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

如果系統中只有單一 PHP 版本，則最後的步驟可以簡化為 `phpenmod sqlsrv pdo_sqlsrv`。 和 `locale-gen` 相同，由於 `phpenmod` 位於 `/usr/sbin` 中，因此您可能需要將此目錄新增到您的 `$PATH`。

### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo service apache2 restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-suse-12-and-15"></a>在 Suse 12 和 15 上安裝驅動程式

> [!NOTE]
> 在下列指示中，使用您的 Suse 版本來取代 `<SuseVersion>`；如果您要使用 Suse Enterprise Linux 15，則它將會是 SLE_15 或 SLE_15_SP1。 針對 Suse 12，請使用 SLE_12_SP4 (或更新版本，若適用的話)。 並非所有 PHP 版本都可供適用於 Suse Linux 的所有版本使用，請參閱 `http://download.opensuse.org/repositories/devel:/languages:/php` 以查看哪些版本的 Suse 具有可用的預設版本 PHP，或 `http://download.opensuse.org/repositories/devel:/languages:/php:/` 以查看哪些其他版本的 PHP 可供哪些版本的 Suse 使用。

> [!NOTE]
> 適用於 PHP 7.4 的套件並不適用於 Suse 12。 若要安裝 PHP 7.2，使用下列 URL 來取代以下的存放庫 URL：`https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`。
> 若要安裝 PHP 7.3，請使用下列 URL 來取代以下的存放庫 URL：`https://download.opensuse.org/repositories/devel:/languages:/php:/php73/<SuseVersion>/devel:languages:php:php73.repo`。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Suse 的 ODBC 驅動程式。

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
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo systemctl restart apache2
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="installing-the-drivers-on-alpine-311"></a>在 Alpine 3.11 上安裝驅動程式

> [!NOTE]
> PHP 的預設版本為 7.3。 Alpine 3.11 的其他存放庫可能會提供其他版本的 PHP。 您可以改為從來源編譯 PHP。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP
適用於 Alpine 的 PHP 套件可以在 `edge/community` 存放庫中找到。 請在其 WIKI 頁面上查看[啟用社群存放庫](https://wiki.alpinelinux.org/wiki/Enable_Community_Repository) \(英文\)。 將下列行新增至 `/etc/apt/repositories`，並以 Alpine 存放庫鏡像的 URL 取代 `<mirror>`：
```
http://<mirror>/alpine/edge/community
```
然後執行：
```
sudo su
apk update
apk add php7 php7-dev php7-pear php7-pdo php7-openssl autoconf make g++
```
### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [Linux 安裝文章](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)上指示來安裝適用於 Alpine 的 ODBC 驅動程式。 

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步驟 3： 安裝適用於 Microsoft SQL Server 的 PHP 驅動程式
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/00_sqlsrv.ini
```

### <a name="step-4-install-apache-and-configure-driver-loading"></a>步驟 4： 安裝 Apache 並設定驅動程式載入
```
sudo apk add php7-apache2 apache2
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo rc-service apache2 restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。


## <a name="installing-the-drivers-on-macos-high-sierra-mojave-and-catalina"></a>在 macOS High Sierra、Mojave 和 Catalina 上安裝驅動程式

如果您尚未安裝，請以如下方式安裝 brew：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安裝 PHP 7.2 或 7.3，請在下列命令中分別使用 php@7.2 或 php@7.3 來取代 php@7.4。

### <a name="step-1-install-php"></a>步驟 1： 安裝 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.4
```
PHP 現在應該位於您的路徑中：執行 `php -v` 以確認您正在執行正確的 PHP 版本。 如果 PHP 不在您的路徑中或不是正確版本，請執行下列命令：
```
brew link --force --overwrite php@7.4
```

### <a name="step-2-install-prerequisites"></a>步驟 2： 安裝必要條件
遵循 [macOS 安裝文章](../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)上指示來安裝適用於 macOS 的 ODBC 驅動程式。 

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
若要尋找 Apache 設定檔 (`httpd.conf`) 以進行 Apache 安裝，請執行 
```
/usr/local/bin/apachectl -V | grep SERVER_CONFIG_FILE
``` 
下列命令會將必要的設定附加到 `httpd.conf`。 請務必將 `/usr/local/etc/httpd/httpd.conf` 取代為上述命令所傳回的路徑：
```
echo "LoadModule php7_module /usr/local/opt/php@7.4/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步驟 5。 重新啟動 Apache 並測試範例指令碼
```
sudo apachectl restart
```
若要測試安裝，請參閱本文件結尾的[測試您的安裝](#testing-your-installation)。

## <a name="testing-your-installation"></a>測試您的安裝

若要測試此範例指令碼，在系統的文件根目錄中建立名為 testsql.php 的檔案。 這在 Ubuntu、Debian 和 Redhat 上為 `/var/www/html/`、在 SUSE 上為 `/srv/www/htdocs`、在 Alpine 上為 `/var/www/localhost/htdocs`，或是在 macOS 上為 `/usr/local/var/www`。 將下列指令碼複製到其中，適當地取代伺服器、資料庫、使用者名稱和密碼。
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
將您的瀏覽器指向 https://localhost/testsql.php (macOS 上的 https://localhost:8080/testsql.php )。 您現在應該能夠連線到您的 SQL Server/Azure SQL 資料庫。

## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[載入 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
