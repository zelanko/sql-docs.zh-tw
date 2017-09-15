---
title: "支援 XML 資料 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f561c72cda30a9f62e202cbd612725d02b7f408
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="supporting-xml-data"></a>支援 XML 資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]提供**xml**資料型別，可讓您儲存 XML 文件和片段中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 **Xml**資料類型是中的內建資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，而且在某些方面類似於其他內建類型，例如**int**和**varchar**。 如同其他內建類型，您可以使用**xml**資料類型作為： 變數類型、 參數類型、 函式傳回型別或資料行時建立的資料表; 或 輸入[!INCLUDE[tsql](../../includes/tsql_md.md)]CAST 和 CONVERT 函數。 在 JDBC 驅動程式， **xml**資料型別可以對應為字串、 位元組陣列、 資料流、 CLOB、 BLOB 或 SQLXML 物件。 字串為預設對應。  
  
 JDBC 驅動程式提供 JDBC 4.0 API 的支援，此 API 引進 SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML**是 JDBC 4.0 資料類型，則會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**資料型別。 因此，若要在應用程式中使用 SQLXML 資料類型，您必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。 如果應用程式在存取 SQLXML 物件及其方法時嘗試使用 sqljdbc3.jar，就會擲回例外狀況。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]一定會先將它儲存於資料庫資料行，驗證 XML 資料。 應用程式可以使用**SQLXML**資料類型，因為 JDBC 驅動程式將它對應到**xml**自動的資料型別。 **SQLXML**支援位於 sqljdbc4.jar。 請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)所支援的 JRE 版本清單[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 本節中的主題描述 SQLXML 介面以及如何進行程式設計的**SQLXML**使用 JDBC API 方法的資料類型。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[SQLXML 介面](../../connect/jdbc/sqlxml-interface.md)|描述 SQLXML 介面及其方法。|  
|[使用 SQLXML 進行程式設計](../../connect/jdbc/programming-with-sqlxml.md)|描述如何使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]API 方法來儲存及擷取 XML 資料，並從關聯式資料庫使用**SQLXML** Java 資料類型。 同時包含有關 SQLXML 物件類型的資訊，並提供使用 SQLXML 物件時重要指導方針和限制的清單。|  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
