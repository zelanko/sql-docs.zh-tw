---
title: "載入 PHP SQL 驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 90ba63857ea38481577083d2a85999e789dfcb84
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="loading-the-php-sql-driver"></a>載入 PHP SQL 驅動程式
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題提供將 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 載入 PHP 處理序空間的指示。  
  
有兩個選項可載入驅動程式。 驅動程式可以在 PHP 啟動時載入，或者可以在 PHP 指令碼執行階段載入。  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>將驅動程式檔案移至您的延伸目錄中  
不論您使用哪個程序，第一個步驟都是將驅動程式檔案放入 PHP 執行階段可以找到它的目錄中。 所以，將驅動程式檔案放入 PHP 延伸目錄中。 如需隨 [安裝的驅動程式檔案清單，請參閱](../../connect/php/system-requirements-for-the-php-sql-driver.md) PHP SQL 驅動程式的系統需求 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  
  
如有必要，指定驅動程式檔案的目錄位置，在 PHP 組態檔 (php.ini) 中，使用**extension_dir**選項。 例如，如果您要將驅動程式檔案放在 c:\php\ext 目錄中，請使用此選項：  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>在 PHP 啟動時載入驅動程式  
若要在 PHP 啟動時載入 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，請先將驅動程式檔案移入延伸目錄中。 然後，請遵循下列步驟：  
  
1.  若要啟用**SQLSRV**驅動程式中，修改**php.ini**下列一行加入延伸區段，或修改已經存在的一行：  
  
    在 Windows （此範例會使用 PHP 7 4.0 版執行緒安全驅動程式）： 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    在 Linux （此範例會使用為 PECL 由已安裝的版本）： 
    ```  
    extension=sqlsrv.so  
    ```  
    若要啟用**PDO_SQLSRV**驅動程式中，修改**php.ini**下列一行加入延伸區段，或修改已經存在的一行：  
  
    在 Windows （此範例會使用 PHP 7 4.0 版執行緒安全驅動程式）：
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    在 Linux （此範例會使用為 PECL 由已安裝的版本）：
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  如果您想要使用**PDO_SQLSRV**驅動程式，PHP 資料物件 (PDO) 副檔名必須為可用，做為內建的擴充功能，或做為以動態方式載入擴充功能。 如果您需要以動態方式載入 PDO_SQLSRV 驅動程式，php_pdo.dll （或 on Linux pdo.so） 必須存在於延伸目錄中，而且下行必須在 php.ini 中：

    Windows:  
    ```
    extension=php_pdo.dll  
    ```  
    On Linux:  
    ```
    extension=pdo.so  
    ```  
  
3.  重新啟動 Web 伺服器。  
  
> [!NOTE]  
> 若要判斷是否已成功載入驅動程式，執行指令碼中呼叫[phpinfo （)](http://go.microsoft.com/fwlink/?LinkId=108678)。  
  
如需 **php.ini** 指示詞的詳細資訊，請參閱 [核心 php.ini 指示詞的描述](http://go.microsoft.com/fwlink/?LinkId=105817)。  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>在 PHP 指令碼執行階段載入驅動程式  
若要在指令碼執行階段載入 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，請先將驅動程式檔案移入延伸目錄中。 然後加入下列這行開頭的比對驅動程式的檔案名稱的 PHP 指令碼：  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
如需與動態載入延伸模組相關的 PHP 函數的詳細資訊，請參閱[dl](http://go.microsoft.com/fwlink/?LinkId=105818)和[extension_loaded。](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>請參閱＜  
[PHP SQL 驅動程式快速入門](../../connect/php/getting-started-with-the-php-sql-driver.md)
[安裝的驅動程式檔案清單，請參閱](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
