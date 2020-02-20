---
title: 使用 JDBC 驅動程式管理結果集 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 273a03e088036057f6d7b31c98074391138de07e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027916"
---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>使用 JDBC 驅動程式管理結果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  結果集代表從資料來源傳回的一組資料，通常是作為查詢的結果。 結果集包含用來保留所要求之資料元素的資料列和資料行，它是以資料指標來導覽。 結果集可以更新，這表示它可加以修改，並將那些修改發送到原始資料來源。 結果集對於基礎資料來源中的變更，也可以有不同的敏感性層級。  
  
 結果集的類型是在建立陳述式時決定，也就是呼叫 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法時。 結果集的基礎角色是要提供 Java 應用程式可用的資料庫資料表示法。 這一點通常是以對結果集資料元素使用具類型的 getter 和 setter 方法來完成。  
  
 下列範例是以 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫為基礎，透過呼叫 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法來建立結果集。 接著使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 類別的 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法來顯示結果集的資料。  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 本節的主題說明結果集使用方式的各方面，包括資料指標類型、並行性和資料列鎖定。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[了解資料指標類型](../../connect/jdbc/understanding-cursor-types.md)|描述 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援的不同資料指標類型。|  
|[了解並行控制](../../connect/jdbc/understanding-concurrency-control.md)|描述 JDBC Driver 支援並行控制的方式。|  
|[了解資料列鎖定](../../connect/jdbc/understanding-row-locking.md)|描述 JDBC 驅動程式支援資料列鎖定的方式。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
