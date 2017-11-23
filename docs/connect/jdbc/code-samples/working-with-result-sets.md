---
title: "使用結果集 |Microsoft 文件"
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
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 840bf63c87a6f6b91e1be3afb690ca62906dc703
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-result-sets"></a>使用結果集
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當您使用包含的資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫操作資料的一種方法是使用結果集。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]支援使用結果集透過[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。 藉由使用 SQLServerResultSet 物件，您可以擷取從 SQL 陳述式或預存程序傳回的資料、 視需要更新的資料和保存資料存回資料庫。  
  
 此外，SQLServerResultSet 物件會提供方法來瀏覽其資料的資料列、 取得或設定它所包含的資料以及對基礎資料庫中建立各種變更的敏感性層級。  
  
> [!NOTE]  
>  如需管理結果集，包括其敏感性的變更，請參閱[JDBC 驅動程式管理結果集](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。  
  
 本節中的主題說明不同的方式，您可以使用結果集處理中所包含的資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[擷取結果集資料範例](../../../connect/jdbc/retrieving-result-set-data-sample.md)|描述如何使用結果集，從中擷取資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫並將其顯示。|  
|[修改結果集資料範例](../../../connect/jdbc/modifying-result-set-data-sample.md)|描述如何使用結果集，插入、 擷取和修改中的資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。|  
|[快取結果集資料範例](../../../connect/jdbc/caching-result-set-data-sample.md)|描述如何使用結果集要擷取大量資料從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫，以及控制如何在用戶端快取該資料。|  
  
## <a name="see-also"></a>請參閱＜  
 [範例 JDBC 驅動程式應用程式](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
