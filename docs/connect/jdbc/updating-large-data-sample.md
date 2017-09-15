---
title: "更新大型資料範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 40444e396dd6efc166acf8b3a45611a24e40d20e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updating-large-data-sample"></a>更新大型資料範例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]範例應用程式示範如何更新資料庫中的大型資料行。  
  
 此範例的程式碼檔案名稱為 updateLargeData.java，可以在下列位置找到：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\adaptive  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您將需要存取[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 您也必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 這個範例會使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)和[unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)導入了 JDBC 4.0 API 來存取驅動程式特有的回應緩衝方法的方法。 若要編譯並執行此範例，您將需要使用 sqljdbc4.jar 類別庫，以便提供 JDBC 4.0 的支援。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會連接到[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]資料庫。 然後，範例程式碼會建立陳述式物件，並使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)方法，檢查陳述式的物件是否為指定的包裝函式[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 [Unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)方法用來存取驅動程式特有的回應緩衝方法。  
  
 接下來，範例程式碼中設定的回應緩衝模式為"**適應性**」 使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別以及示範如何取得適應性緩衝模式。  
  
 然後，執行 SQL 陳述式，並且將它傳回成為可更新的資料放[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
 最後，範例程式碼會逐一查看包含在結果集中的資料列。 如果它找到空的文件摘要，它會使用組合[updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)和[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法來更新資料的資料列，並再次將它保存到資料庫。 如果已經有資料，它會使用[getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法以顯示一些它所包含的資料。  
  
 驅動程式的預設行為是"**適應性。**" 不過，為順向可更新結果集，而且結果集中的資料大小超過應用程式記憶體時，應用程式必須使用明確設定適應性緩衝模式[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法的[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。  
  
 [!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用大型資料](../../connect/jdbc/working-with-large-data.md)  
  
  
