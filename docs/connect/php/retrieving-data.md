---
title: 擷取資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbc6d4e971a810d581b8ace2de8fd7882171c460
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676056"
---
# <a name="retrieving-data"></a>擷取資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此主題和本節中的主題將討論如何擷取資料。  
  
## <a name="sqlsrv-driver"></a>SQLSRV 驅動程式  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驅動程式提供下列從結果集內擷取資料的選項：  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> 當您使用任何先前所述的函數時，請避免以 Null 比較做為結束迴圈的準則。 由於 **sqlsrv** 函數會在錯誤發生時傳回 false，下列程式碼可能會在 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)中出現錯誤時造成無限迴圈：  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
如果您的查詢擷取多個結果集，您可以透過 [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)移至下一個結果集。  
  
從 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 1.1 版開始，您可以使用 [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) 來查看結果集是否有資料列。  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 PDO_SQLSRV 驅動程式提供下列從結果集內擷取資料的選項：  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
如果您的查詢擷取多個結果集，您可以透過 [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md)移至下一個結果集。  
  
如果您指定可捲動的資料指標，然後呼叫 [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md)，您可以查看結果集內有多少資料列。  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) 可讓您指定資料指標類型。 然後，您可以透過 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 選取資料列。 如需範例和詳細資訊，請參閱 [PDO::prepare](../../connect/php/pdo-prepare.md) 。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|---------|---------------|  
|[以資料流的形式擷取資料](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|概略說明如何從伺服器串流處理資料，並提供特定使用案例的連結。|  
|[使用方向參數](../../connect/php/using-directional-parameters.md)|說明如何在呼叫預存程序時使用參數方向。|  
|[指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|示範如何建立結果集，您可以依任何順序存取的資料列。|  
|[如何：使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|說明如何使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型。|  
|[如何： 擷取為 PHP Datetime 物件，使用 PDO_SQLSRV 驅動程式的日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)|描述如何使用 PDO_SQLSRV 驅動程式的物件形式擷取日期和時間類型。|  
|[使用 SQLSRV 驅動程式的格式化十進位字串](../../connect/php/formatting-decimals-sqlsrv-driver.md)|示範如何設定使用 SQLSRV 驅動程式的十進位或貨幣值的格式。|  
|[使用 PDO_SQLSRV 驅動程式的格式化十進位字串](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)|示範如何設定使用 PDO_SQLSRV 驅動程式的十進位或貨幣值的格式。|  
  
## <a name="related-sections"></a>相關章節  
[如何：指定 PHP 資料類型](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>另請參閱  
[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)  
  
