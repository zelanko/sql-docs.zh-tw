---
title: 關於文件中的程式碼範例 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1520106fa39e850bf09d78a5eeee955fba1260fb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606738"
---
# <a name="about-code-examples-in-the-documentation"></a>關於文件中的程式碼範例
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>關於程式碼範例的註解
執行 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 文件中的程式碼範例時，須留意幾項要點：  
  
-   幾乎所有的範例假設 SQL Server 2008 或更新版本和 AdventureWorks 資料庫安裝在本機電腦上。  
  
    如需如何下載 SQL Server 免費版和試用版的相關資訊，請參閱 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193)。  
  
    如需有關如何下載並安裝 AdventureWorks 資料庫的資訊，請參閱 < [SQL Server 範例 Github 儲存機制中的 AdventureWorks 頁面](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)。
  
-   本文件中幾乎所有的程式碼範例均應從命令列執行，如此可讓所有程式碼範例的測試自動化。 如需如何從命令列執行 PHP 的相關資訊，請參閱 [從命令列使用 PHP](https://php.net/manual/en/features.commandline.php)。  
  
-   雖然這些範例旨在從命令列執行，但每個範例都可以從瀏覽器叫用來執行，且無須對指令碼進行任何變更。 若要妥善格式化輸出，以取代每個"\n""\<\/b >"之前從瀏覽器叫用每個範例中。  
  
-   為了讓每個範例專注在其重點上，我們並未在所有範例中執行正確的錯誤處理。 建議您檢查任何對 **sqlsrv** 函數或 PDO 方法的呼叫是否有錯誤，並根據應用程式的需求予以處理。  
  
    發生錯誤時，您可以透過下列程式碼行結束指令碼，以取得錯誤資訊：  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    或者，如果您使用 PDO，  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    如需關於處理錯誤和警告的詳細資訊，請參閱 [處理錯誤和警告](../../connect/php/handling-errors-and-warnings.md)。  
  
## <a name="see-also"></a>另請參閱  
[Microsoft Drivers for PHP for SQL Server 概觀](../../connect/php/overview-of-the-php-sql-driver.md)
  
