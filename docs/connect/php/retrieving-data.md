---
title: "擷取資料 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6cee44ce2e24055285b56b7889902166d460f1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
  
從 1.1 版中[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，您可以使用[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)來查看結果集是否有資料列。  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式  
PDO_SQLSRV 驅動程式的[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]提供下列從結果集內擷取資料的選項：  
  
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
|[指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|示範在使用 SQLSRV 驅動程式時，如何建立您可以用任何順序存取資料列的結果集。|  
|[如何：使用 SQLSRV 驅動程式，以字串的形式擷取日期和時間類型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|說明如何以字串的形式擷取日期和時間類型。|  
  
## <a name="related-sections"></a>相關章節  
[如何：指定 PHP 資料類型](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[擷取資料](../../connect/php/retrieving-data.md)  
  

