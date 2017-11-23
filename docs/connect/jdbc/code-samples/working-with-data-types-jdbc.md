---
title: "使用資料類型 (JDBC) |Microsoft 文件"
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
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 669ce17e79da30344a33e8c44b4e548099c4bae1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-data-types-jdbc"></a>使用資料類型 (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  主要功能[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]可讓 Java 開發人員能夠存取包含在資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。 為了達成此目的，JDBC 驅動程式會調解之間的轉換[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型和 Java 語言類型與物件。  
  
> [!NOTE]  
>  如需詳細的討論[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和 JDBC driver 資料類型，包括其差異和它們如何轉換為 Java 語言資料類型，請參閱[了解 JDBC Driver 資料類型](../../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
 為了能夠使用 SQL Server 資料類型，JDBC 驅動程式提供取得\<類型 >，並設定\<類型 > 的方法[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別，並可提供取得\<類型 > 及更新\<類型 > 的方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別。 使用哪一種方法視您正要使用的資料類型而定，以及是否會使用結果集或查詢。  
  
 本節中的主題描述如何使用 JDBC driver 資料類型來存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Java 應用程式中的資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[基本資料類型範例](../../../connect/jdbc/basic-data-types-sample.md)|描述如何使用結果集 getter 方法擷取基本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型值，以及如何使用結果集 update 方法更新那些值。|  
|[SQLXML 資料類型範例](../../../connect/jdbc/sqlxml-data-type-sample.md)|描述如何在關聯式資料庫中儲存 XML 資料、 如何從資料庫擷取 XML 資料以及如何剖析具有 XML 資料**SQLXML** Java 資料類型。|  
  
## <a name="see-also"></a>請參閱＜  
 [範例 JDBC 驅動程式應用程式](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
