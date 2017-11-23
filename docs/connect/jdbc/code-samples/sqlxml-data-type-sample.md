---
title: "SQLXML 資料類型範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: ffd9ba36871ff40eca7b61b02503f979d9aa30c7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="sqlxml-data-type-sample"></a>SQLXML 資料類型範例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]範例應用程式示範如何在關聯式資料庫中儲存 XML 資料、 如何從資料庫擷取 XML 資料，以及如何剖析具有 XML 資料**SQLXML** Java 資料類型。  
  
 本節中的程式碼範例會使用 Simple API for XML (SAX) 剖析器。 SAX 是一套公開開發的標準，可用於以事件為基礎的方式剖析 XML 文件。 此外，它也會提供用於使用 XML 資料的應用程式開發介面。 請注意，應用程式也可以使用任何其他 XML 剖析器，例如文件物件模型 (DOM) 或 Streaming API for XML (StAX)。  
  
 文件物件模型 (DOM) 會提供 XML 文件、片段、節點或節點集的程式表示法。 此外，它也會提供用於使用 XML 資料的應用程式開發介面。 同樣地，Streaming API for XML (StAX) 是以 Java 為基礎的 API，可用於提取剖析 XML。  
  
> [!IMPORTANT]  
>  若要使用 SAX 剖析器 API，您必須從 javax.xml 封裝匯入標準 SAX 實作。  
  
 此範例的程式碼檔案名稱為 sqlxmlExample.java，可以在下列位置找到：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\datatypes  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的例外狀況。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
 此外，您需要存取[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫來執行此範例應用程式。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會連接到[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]資料庫，然後再叫用 createSampleTables 方法。  
  
 createSampleTables 方法會卸除 TestTable1 和 TestTable2 測試資料表 (如果它們存在的話)。 然後，它會將兩個資料列插入 TestTable1 中。  
  
 此外，程式碼範例包含下列三種方法以及一個名為 ExampleContentHandler 的額外類別。  
  
 ExampleContentHandler 類別會實作針對剖析器事件定義方法的自訂內容處理常式。  
  
 showGetters 方法將示範如何使用 SAX、ContentHandler 和 XMLReader 來剖析 SQLXML 物件中的資料。 首先，程式碼範例會建立自訂內容處理常式的執行個體，亦即 ExampleContentHandler。 接著，它會建立並執行從 TestTable1 中傳回一組資料的 SQL 陳述式。 然後，程式碼範例會取得 SAX 剖析器並剖析 XML 資料。  
  
 ShowSetters 方法將示範如何設定**xml**使用 SAX、 ContentHandler 和 ResultSet 資料行。 首先會建立空的 SQLXML 物件使用[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Connection 類別的方法。 然後，它會取得內容處理常式的執行個體，以便將資料寫入 SQLXML 物件中。 接著，程式碼範例會將資料寫入 TestTable1。 最後，範例程式碼，逐一查看結果集中包含的資料列並使用[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)方法來讀取 XML 資料。  
  
 showTransformer 方法將示範如何從某份資料表中取得 XML 資料，然後使用 SAX 和 Transformer，將該 XML 資料插入另一份資料表中。 首先，它會從 TestTable1 中擷取來源 SQLXML 物件。 然後，它會建立空的目的地 SQLXML 物件使用[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Connection 類別的方法。 接著，它會更新目的地 SQLXML 物件並將 XML 資料寫入 TestTable2。 最後，範例程式碼，逐一查看結果集中包含的資料列並使用[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)方法來讀取 TestTable2 中的 XML 資料。  
  
 [!code[JDBC#UsingSQLXML1](../../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]  
  
## <a name="see-also"></a>請參閱＜  
 [使用資料類型 &#40;JDBC &#41;](../../../connect/jdbc/working-with-data-types-jdbc.md)  
  
  
