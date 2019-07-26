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
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936386"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>載入 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本頁提供將 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 載入 PHP 處理序空間的指示。  
  
您可以從適用于 PHP for SQL Server Github 專案頁面的[Microsoft 驅動程式](https://github.com/Microsoft/msphpsql/releases)下載適用于您平臺的預建驅動程式。 每個安裝套件都包含以執行緒和非執行緒形式變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 上, 它們也可以在32位和64位的變數中使用。 如需每個套件中包含的驅動程式檔案清單, 請參閱適用于[PHP 的 Microsoft 驅動程式 SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)。 驅動程式檔案必須符合 PHP 環境的 PHP 版本、架構和 threadedness。

在 Linux 和 macOS 上, 您也可以使用 PECL 來安裝驅動程式, 如[安裝教學](../../connect/php/installation-tutorial-linux-mac.md)課程中所找到。

您也可以在建立 PHP 或使用`phpize`時, 從來源建立驅動程式。 如果您選擇從來源建立驅動程式, 您可以選擇將它們以靜態方式建立到 PHP, 而不是藉由將 (在`--enable-sqlsrv=static --with-pdo_sqlsrv=static` Linux 和 macOS 上) 或`--enable-sqlsrv=static --with-pdo-sqlsrv=static` ( `./configure`在 Windows 上) 新增至命令, 而將其建立為共用擴充功能建立 PHP。 如需 php 組建系統和`phpize`的詳細資訊, 請參閱[php 檔](http://php.net/manual/install.php)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>將驅動程式檔案移至您的延伸目錄中  
驅動程式檔案必須位於 PHP 執行時間可以找到的目錄中。 最簡單的方式是將驅動程式檔案放在您的預設 PHP 延伸目錄中, 以尋找預設`php -i | sls extension_dir`目錄、在`php -i | grep extension_dir` Windows 或 Linux/macOS 上執行。 如果您不是使用預設的延伸目錄, 請使用**extension_dir**選項, 在 PHP 設定檔 (php .ini) 中指定一個目錄。 例如, 在 Windows 上, 如果您將驅動程式檔案放在`c:\php\ext`目錄中, 請將下面這一行新增至 php .ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 啟動時載入驅動程式  
若要在 PHP 啟動時載入 SQLSRV 驅動程式，請先將驅動程式檔案移入延伸目錄中。 然後，請遵循下列步驟：  
  
1.  若要啟用**SQLSRV**驅動程式, 請將下列程式程式碼新增至延伸區段, 並視需要變更檔案名, 以修改**php。**  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上, 如果您已為散發套件下載預先建立的二進位檔: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果您已從來源或使用 PECL 編譯 SQLSRV 二進位檔, 則會改為將其命名為 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要啟用**PDO_SQLSRV**驅動程式, PHP 資料物件 (PDO) 延伸模組必須是可用的內建延伸模組, 或是以動態方式載入的延伸模組。

    在 Windows 上, 預先建立的 PHP 二進位檔隨附 PDO 內建功能, 因此不需要修改 PHP .ini 就能載入它。 不過, 如果您已從來源編譯 PHP, 並指定要建立的個別 PDO 延伸模組, 則會將其`php_pdo.dll`命名為, 而且您必須將下列程式碼複製到您的延伸模組目錄, 並將下行新增至 PHP .ini:  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上, 如果您已使用系統的套件管理員安裝 PHP, PDO 可能會安裝為名為 pdo.so 的動態載入延伸模組。 PDO 延伸模組必須在 PDO_SQLSRV 擴充功能之前載入, 否則載入將會失敗。 延伸模組通常會使用個別的 .ini 檔案載入, 而這些檔案會在 php .ini 之後讀取。 因此, 如果 pdo.so 是透過自己的 .ini 檔案載入, 則在需要 PDO 之後載入 PDO_SQLSRV 驅動程式的個別檔案。 

    若要找出擴充功能專屬 .ini 檔案的所在目錄, 請執行`php --ini` , 並記下`Scan for additional .ini files in:`所列的目錄。 尋找載入 pdo.so 的檔案--它的前面可能會加上數位, 例如10-pdo。 數值前置詞表示 .ini 檔案的載入順序, 而沒有數值前置詞的檔案則會依字母順序載入。 建立檔案, 以載入名為30-pdo_sqlsrv 的 PDO_SQLSRV 驅動程式檔案 (任何大於以 pdo 或 PDO_SQLSRV 首碼的數位) 或 (如果 PDO .ini 不是以數位做為前置詞), 然後在其中加入下列一行, 將檔案名變更為適當  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    如同 SQLSRV, 如果您已從來源或使用 PECL 編譯 PDO_SQLSRV 二進位檔, 則會改為將它命名為 PDO_SQLSRV。因此:
    ```
    extension=pdo_sqlsrv.so
    ```
    將此檔案複製到包含其他 .ini 檔案的目錄。 

    如果您已使用內建 PDO 支援從來源編譯 PHP, 則不需要個別的 .ini 檔案, 而且您可以將適當的一行新增至 PHP .ini。
  
3.  重新啟動 Web 伺服器。  
  
> [!NOTE]  
> 若要判斷是否已成功載入驅動程式，請執行可呼叫 [phpinfo()](https://php.net/manual/en/function.phpinfo.php) 的指令碼。  
  
如需 **php.ini** 指示詞的詳細資訊，請參閱[核心 php.ini 指示詞的描述](https://php.net/manual/en/ini.core.php)。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
