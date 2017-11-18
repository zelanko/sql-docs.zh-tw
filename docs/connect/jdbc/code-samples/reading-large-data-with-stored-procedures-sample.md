---
title: "讀取大型資料的預存程序範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3ec50f3fcff4098f8a5fe544b4f49b432455782
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="reading-large-data-with-stored-procedures-sample"></a>使用預存程序讀取大型資料範例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]範例應用程式示範如何從預存程序中擷取大型 OUT 參數。  
  
 此範例的程式碼檔案名稱為 executeStoredProcedure.java，可以在下列位置找到：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\adaptive  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您將需要存取[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。 您也必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
 您也必須建立下列預存程序中的[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫：  
  
```  
CREATE PROCEDURE GetLargeDataValue   
  (@Document_ID int,   
   @Document_ID_out int OUTPUT,   
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  
  
AS   
BEGIN    
   SELECT @Document_ID_out = DocumentID,   
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary   
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會連接到[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]資料庫。 接著，範例程式碼會建立範例資料，並使用參數化查詢更新 Production.Document 資料表。 接著，範例程式碼會取得適應性緩衝模式使用[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)類別，並執行 GetLargeDataValue 預存程序。 請注意，從 JDBC Driver 2.0 版開始，responseBuffering 連接屬性預設設定為 "adaptive"。  
  
 最後，程式碼範例顯示利用 OUT 參數傳回的資料，並也會示範如何使用`mark`和`reset`重新讀取資料的任何部分的資料流上的方法。  
  
 [!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用大型資料](../../../connect/jdbc/working-with-large-data.md)  
  
  

