---
title: 使用資料類型 (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d5f4414e596ab59f33ab73b6d01908b16d89b24
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923918"
---
# <a name="working-with-data-types-jdbc"></a>使用資料類型 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的主要功能就是可讓 Java 開發人員存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中包含的資料。 為了完成這項工作，JDBC 驅動程式會調解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型和 Java 語言類型與物件之間的轉換。  
  
> [!NOTE]  
> 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 JDBC 驅動程式資料類型的詳細討論，包括其差異與它們如何轉換為 Java 語言資料類型，請參閱[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
為了能夠使用 SQL Server 資料類型，JDBC 驅動程式提供 get\<類型> 和 set\<類型>方法給 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別，它也提供 get\<類型> 和 update\<類型> 方法給 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 類別。 使用哪一種方法視您正要使用的資料類型而定，以及是否會使用結果集或查詢。  
  
本節的主題描述如何使用 JDBC 驅動程式資料類型，在 Java 應用程式中存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[基本資料類型範例](../../connect/jdbc/basic-data-types-sample.md)|描述如何使用結果集 getter 方法來擷取基本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型值，以及如何使用結果集 update 方法來更新這些值。|  
|[SQLXML 資料類型範例](../../connect/jdbc/sqlxml-data-type-sample.md)|描述如何在關聯式資料庫中儲存 XML 資料、如何從資料庫中擷取 XML資料，以及如何剖析具有 **SQLXML** Java 資料類型的 XML資料。|  
|[空間資料類型範例](../../connect/jdbc/spatial-data-types-sample.md)|描述如何使用 Microsoft JDBC 驅動程式定義的 Java 類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Geometry**和**Geography **，儲存和擷取**  資料庫中具有空間資料類型 'Geometry' 和 'Geography' 的資料。|

## <a name="see-also"></a>另請參閱

[範例 JDBC 驅動程式應用程式](../../connect/jdbc/sample-jdbc-driver-applications.md)  
