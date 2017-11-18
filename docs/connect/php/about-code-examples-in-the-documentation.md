---
title: "關於文件中的程式碼範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d24d29aba9db9d3626a456f87f799e00da1b42cc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="about-code-examples-in-the-documentation"></a>關於文件中的程式碼範例
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

執行 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 文件中的程式碼範例時，須留意幾項要點：  
  
-   幾乎所有範例都假設已在本機電腦上安裝 SQL Server 2005 或更新版本 (如果使用 3.1 版，則為 SQL Server 2008 或更新版本) 和 AdventureWorks 資料庫。  
  
    如需如何下載 SQL Server 免費版和試用版的相關資訊，請參閱 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193)。  
  
    如需如何下載 AdventureWorks 資料庫的相關資訊，請參閱 [Microsoft SQL Server 範例和社群專案](http://go.microsoft.com/fwlink/?LinkID=67739)。  
  
    如需如何安裝 AdventureWorks 資料庫的相關資訊，請參閱 [逐步解說：安裝 AdventureWorks 資料庫](http://go.microsoft.com/fwlink/?LinkID=65819)。  
  
-   本文件中幾乎所有的程式碼範例均應從命令列執行，如此可讓所有程式碼範例的測試自動化。 如需如何從命令列執行 PHP 的相關資訊，請參閱 [從命令列使用 PHP](http://php.net/manual/en/features.commandline.php)。  
  
-   雖然撰寫成從命令列執行，但每個範例都可以從瀏覽器呼叫而執行，且無須對指令碼進行任何變更。 若要達到最理想的輸出格式，以取代每個"\n""\<\/b >"中每個範例，再予以叫用從瀏覽器。  
  
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
[PHP SQL 驅動程式概觀](../../connect/php/overview-of-the-php-sql-driver.md)
  

