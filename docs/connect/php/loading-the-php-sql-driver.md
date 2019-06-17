---
title: 載入 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4b2f02fc81b969f8633a5a951483745c1d2635b0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799643"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>載入 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本頁提供將 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 載入 PHP 處理序空間的指示。  
  
您可以下載預先建置的驅動程式，您的平台，從[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 專案頁面。 每個安裝套件包含執行緒及非執行緒變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 中，它們也會提供 32 位元和 64 位元的變體。 請參閱[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)如需每個封裝中包含的驅動程式檔案的清單。 PHP 版本、 架構及 PHP 環境的 threadedness，必須符合的驅動程式檔案。

在 Linux 和 macOS 上，安裝驅動程式可以或者使用 PECL，在中找到[安裝教學課程](../../connect/php/installation-tutorial-linux-mac.md)。

您也可以建立從來源驅動程式，建置 PHP 時或使用`phpize`。 如果您選擇建置來源的驅動程式，您可以選擇建置靜態到 PHP 而不要加上建立共用延伸模組`--enable-sqlsrv=static --with-pdo_sqlsrv=static`（在 Linux 和 macOS） 或`--enable-sqlsrv=static --with-pdo-sqlsrv=static`（在 Windows 中) 至`./configure`命令建立 PHP。 如需有關 PHP 組建系統以及`phpize`，請參閱 < [PHP 文件](http://php.net/manual/install.php)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>將驅動程式檔案移至您的延伸目錄中  
驅動程式檔案必須位於為 PHP 執行階段可以找到的目錄。 它是最簡單的方式將驅動程式檔案放在預設 PHP 延伸目錄-若要尋找預設目錄，請執行`php -i | sls extension_dir`在 Windows 上或`php -i | grep extension_dir`在 Linux/macOS 上。 如果您未使用的預設延伸模組目錄，指定的目錄，在 PHP 組態檔 (php.ini) 中，使用**extension_dir**選項。 例如，在 Windows 中，如果您已將驅動程式檔案放在您`c:\php\ext`目錄中，將下面這一行加入至 php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 啟動時載入驅動程式  
若要在 PHP 啟動時載入 SQLSRV 驅動程式，請先將驅動程式檔案移入延伸目錄中。 然後，請遵循下列步驟：  
  
1.  若要啟用**SQLSRV**驅動程式，修改**php.ini**下面這一行加入延伸區段，變更為適當的檔案名稱：  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上，如果您已下載預先建置的二進位檔，為您的散發： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果您編譯 SQLSRV 二進位從來源或 PECL，其會改為 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要啟用**PDO_SQLSRV**驅動程式的 PHP 資料物件 (PDO) 延伸模組必須可用，做為內建的擴充功能，或以動態方式載入的延伸模組。

    在 Windows、 預先建置的 PHP 二進位檔隨附 PDO 內建功能，這樣就不需要修改 php.ini 載入它。 如果，不過，您已編譯 PHP 來源，並指定個別的 PDO 延伸功能，來建置，它將會命名為`php_pdo.dll`，而且您必須將它複製到您的延伸模組目錄，並將下列這一行加入至 php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上，如果您已安裝使用您系統的套件管理員 中，PHP PDO 可能安裝為具名 pdo.so 動態載入延伸模組。 PDO 延伸模組必須載入 PDO_SQLSRV 延伸模組之前，或載入將會失敗。 會載入延伸模組通常使用的個別.ini 檔案，並且這些檔案被讀取之後 php.ini。 因此，如果 pdo.so 透過自己的.ini 檔案載入，則需要 PDO 之後載入 PDO_SQLSRV 驅動程式的個別檔案。 

    若要了解目錄延伸模組特定.ini 檔案的位置，執行`php --ini`並記下目錄底下所列`Scan for additional .ini files in:`。 找到的檔案，載入 pdo.so--它可能是加上數字，例如 10 pdo.ini。 數值的前置詞表示.ini 檔案的載入順序，而不需要數值的前置詞的檔案會依字母順序載入。 建立檔案以載入 PDO_SQLSRV 驅動程式檔案，稱為 30 pdo_sqlsrv.ini （任何數字大於的前置詞 pdo.ini 運作） 或 pdo_sqlsrv.ini （如果 pdo.ini 不加上數字），並新增下面這一行，變更為檔案名稱適當的：  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    為與 SQLSRV，如果您編譯 PDO_SQLSRV 二進位從來源或 PECL，它會改為會命名為 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    這個檔案複製到包含其他的.ini 檔案的目錄。 

    如果您已從來源使用內建的 PDO 支援 PHP，您不需要的個別.ini 檔，您可以將適當的程式行上方加入 php.ini。
  
3.  重新啟動 Web 伺服器。  
  
> [!NOTE]  
> 若要判斷是否已成功載入驅動程式，請執行可呼叫 [phpinfo()](https://php.net/manual/en/function.phpinfo.php) 的指令碼。  
  
如需 **php.ini** 指示詞的詳細資訊，請參閱[核心 php.ini 指示詞的描述](https://php.net/manual/en/ini.core.php)。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
