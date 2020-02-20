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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936386"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>載入 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本頁提供將 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 載入 PHP 處理序空間的指示。  
  
您可以從 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) \(英文\) GitHub 專案頁面，下載適用於您的平台的預先建置驅動程式。 每個安裝套件都包含執行緒和非執行緒形式變體的 SQLSRV 和 PDO_SQLSRV 驅動程式檔案。 在 Windows 上，其也以 32 位元與 64 位元變體提供。 請參閱 [Microsoft Drivers for PHP for SQL Server 的系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)以取得包含在每個套件中的驅動程式檔案清單。 驅動程式檔案必須符合您 PHP 環境的 PHP 版本、架構及執行緒狀態。

在 Linux 和 macOS 上，可以改為使用 PECL 來安裝驅動程式，如[安裝教學課程](../../connect/php/installation-tutorial-linux-mac.md)中所述。

您也可以在建置 PHP 時，或是使用 `phpize` 來從來源建置驅動程式。 如果您選擇從來源建置驅動程式，您可以透過在建置 PHP 時將 `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (於 Linux 和 macOS 上) 或 `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (於 Windows 上) 命令新增至 `./configure` 命令，來選擇以靜態方式將其建置到 PHP 中，而非將其建置為共用擴充。 如需 PHP 建置系統和 `phpize` 的詳細資訊，請參閱 [PHP 文件](http://php.net/manual/install.php) \(英文\)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>將驅動程式檔案移至您的延伸目錄中  
驅動程式檔案必須位於 PHP 執行階段可找到的目錄中。 最簡單的方式是將驅動程式檔案置於您的預設 PHP 擴充目錄。若要尋找預設目錄，請在 Windows 上執行 `php -i | sls extension_dir`，或在 Linux/macOS 上執行 `php -i | grep extension_dir`。 如果您不使用預設擴充目錄，請使用 **extension_dir** 選項在 PHP 設定檔 (php.ini) 中指定目錄。 例如，在 Windows 上，如果您將驅動程式檔案置於 `c:\php\ext` 目錄中，請將下列行新增至 php.ini：
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 啟動時載入驅動程式  
若要在 PHP 啟動時載入 SQLSRV 驅動程式，請先將驅動程式檔案移入延伸目錄中。 然後，請遵循下列步驟：  
  
1.  若要啟用 **SQLSRV** 驅動程式，請修改 **php.ini**，方法是將下列行新增至擴充區段，並適當地變更檔案名稱：  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上，如果您已下載適用於您發行版本的預先建置二進位檔： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果您已從來源或搭配 PECL 編譯 SQLSRV 二進位檔，系統會改為將其命名為 sqlsrv.so：
    ```
    extension=sqlsrv.so
    ```
  
2.  若要啟用 **PDO_SQLSRV** 驅動程式，PHP 資料物件 (PDO) 擴充必須可供使用，無論是以內建擴充的形式，還是以動態方式載入之擴充的形式。

    在 Windows 上，預先建置的 PHP 二進位檔已內建 PDO，因此不需要修改 php.ini 便能加以載入。 不過，如果您已從來源編譯 PHP 並指定個別的 PDO 擴充來加以建置，其名稱將會是 `php_pdo.dll`，且您必須將其複製到您的擴充目錄，並將下列行新增至 php.ini：  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上，如果您已使用系統的套件管理員安裝 PHP，PDO 可能已經以名為 pdo.so 之動態載入擴充的形式安裝。 PDO 擴充必須在 PDO_SQLSRV 擴充之前載入，否則載入將會失敗。 擴充通常會使用個別的 .ini 檔案載入，且這些檔案會在 php.ini 之後讀取。 因此，如果 pdo.so is 是透過其自己的 .ini 檔案載入，在 PDO 之後便需要載入 PDO_SQLSRV 驅動程式的個別檔案。 

    若要找出擴充特定的 .ini 檔案位於哪個目錄，請執行 `php --ini` 並記下列於 `Scan for additional .ini files in:` 底下的目錄。 找出載入 pdo.so 的檔案，其名稱前端很可能會有號碼，例如 10-pdo.ini。 數值前置詞會指出 .ini 檔案的載入順序，而不具有數值前置詞的檔案則會以字母順序載入。 建立載入 PDO_SQLSRV 驅動程式檔案的檔案，並將其命名為 30-pdo_sqlsrv.ini (大於 pdo.ini 數值前置詞的任何數字皆可) 或 pdo_sqlsrv.ini (如果 pdo.ini 沒有數值前置詞的話)，然後為其新增下列行，並適當地變更檔案名稱：  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    和 SQLSRV 相同，如果您已從來源或搭配 PECL 編譯 PDO_SQLSRV 二進位檔，系統會改為將其命名為 pdo_sqlsrv.so：
    ```
    extension=pdo_sqlsrv.so
    ```
    將此檔案複製到包含其他 .ini 檔案的目錄。 

    如果您已搭配內建 PDO 支援從來源編譯 PHP，便不需要個別的 .ini 檔案，且您可以將上述適當的行新增至 php.ini。
  
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
  
