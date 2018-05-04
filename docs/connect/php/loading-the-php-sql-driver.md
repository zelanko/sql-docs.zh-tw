---
title: 載入 Microsoft Drivers for PHP for SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c29424ef266d627e2194a309da54741bc170ae27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>載入 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本頁面提供的指示來載入[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]PHP 處理序空間。  
  
您可以下載預先建立的驅動程式從您為平台[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 專案頁面中。 每個安裝套件包含在執行緒和執行緒非 variant SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 中，它們也會提供 32 位元和 64 位元變數。 請參閱[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)如需每個封裝中所包含的驅動程式檔案的清單。 PHP 版本、 架構和 threadedness 的 PHP 環境，必須符合的驅動程式檔案。

在 Linux 和 macOS，驅動程式可以或者安裝中找到使用 PECL，[安裝教學課程](../../connect/php/installation-tutorial-linux-mac.md)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>將驅動程式檔案移至您的延伸目錄中  
驅動程式檔案必須位於 PHP 執行階段可以找到的目錄。 最為簡單，驅動程式檔案放入預設 PHP 延伸目錄-若要尋找的預設目錄，執行`php -i | sls extension_dir`Windows 上或`php -i | grep extension_dir`Linux/macOS 上。 如果您不使用預設的延伸模組目錄，指定一個目錄在 PHP 組態檔 (php.ini) 中，使用**extension_dir**選項。 例如，在 Windows 中，如果您已將驅動程式檔案放在您`c:\php\ext`目錄中，將下列行加入至 php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 啟動時載入驅動程式  
若要載入的 SQLSRV 驅動程式，PHP 啟動時，先將驅動程式檔案移入延伸目錄中。 然後，請遵循下列步驟：  
  
1.  若要啟用**SQLSRV**驅動程式中，修改**php.ini**由下列一行加入延伸區段中，變更為適當的檔案名稱：  
  
    Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    On Linux，如果您已下載的預先建置的二進位檔散發： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果您要編譯 SQLSRV 二進位從來源或 PECL，其會改為 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要啟用**PDO_SQLSRV**驅動程式，PHP 資料物件 (PDO) 副檔名必須為可用，做為內建的擴充功能，或做為以動態方式載入擴充功能。

    在 Windows 中，預先建立的 PHP 二進位檔隨附 PDO 內建功能，因此不需要修改 php.ini 載入它。 如果，不過，已編譯的 PHP 來源，然後指定個別的 PDO 擴充功能來建置，其會為`php_pdo.dll`，而且您必須將它複製到您的延伸目錄，並將下列行加入至 php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    On Linux，如果您已安裝使用您系統的封裝管理員 中，PHP PDO 可能安裝為具名 pdo.so 動態載入延伸模組。 PDO 延伸模組必須載入 PDO_SQLSRV 延伸模組之前，或載入將會失敗。 載入延伸模組是通常使用的個別.ini 檔案之後 php.ini, 會讀取這些檔案。 因此，如果 pdo.so 透過自己的.ini 檔案載入時，則需要 PDO 之後載入 PDO_SQLSRV 驅動程式的個別檔案。 

    若要找出哪個目錄延伸模組特定.ini 檔案的位置，執行`php --ini`並記下所列出的目錄`Scan for additional .ini files in:`。 尋找的檔案，載入 pdo.so--可能是由數字，例如 10 pdo.ini 前置詞。 數值的前置詞表示.ini 檔案的載入順序，而沒有數值的前置詞的檔案會依字母順序載入。 建立檔案以載入 PDO_SQLSRV 驅動程式檔案，稱為 30 pdo_sqlsrv.ini （任何數字大於的前置詞 pdo.ini works） 或 pdo_sqlsrv.ini （如果 pdo.ini 不加上數字），並加入下列行，變更為檔名適當的：  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    做為與 SQLSRV，如果您要編譯 PDO_SQLSRV 二進位從來源或 PECL，其會改為名稱為 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    將這個檔案複製到包含其他.ini 檔案的目錄。 

    如果您要編譯 PHP 來源使用內建 PDO 支援，您不需要的個別.ini 檔，您可以將適當的程式行上方加入 php.ini。
  
3.  重新啟動 Web 伺服器。  
  
> [!NOTE]  
> 若要判斷是否已成功載入驅動程式，執行指令碼中呼叫[phpinfo （)](http://php.net/manual/en/function.phpinfo.php)。  
  
如需有關**php.ini**指示詞，請參閱[核心 php.ini 指示詞的描述](http://php.net/manual/en/ini.core.php)。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[系統需求的 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[程式程式設計指南 Microsoft Drivers for PHP，適用於 SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
