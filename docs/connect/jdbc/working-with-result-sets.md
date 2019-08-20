---
title: 使用結果集 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d38cb92fbbf83f9b8a110d2e17f60af70c177ab4
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025443"
---
# <a name="working-with-result-sets"></a>使用結果集

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中包含的資料時，一種操作資料的方法就是使用結果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援透過 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件來使用結果集。 藉由使用 SQLServerResultSet 物件，您可以擷取從 SQL 陳述式或預存程序傳回的資料、依需要更新資料，然後將該資料存回資料庫。  
  
此外，SQLServerResultSet 物件也提供數種方法，可用來瀏覽其資料列、取得或設定其包含的資料，以及對基礎資料庫中的變更建立各種敏感性層級。  
  
> [!NOTE]  
> 如需管理結果集的詳細資訊, 包括其對變更的敏感度, 請參閱[使用 JDBC 驅動程式管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。  
  
本節的主題描述您可以使用結果集，操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中所包含資料的不同方法。  
  
## <a name="in-this-section"></a>本節內容  
  
| 主題                                                                                        | 描述                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [擷取結果集資料範例](../../connect/jdbc/retrieving-result-set-data-sample.md) | 描述如何使用結果集，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取資料並顯示資料。                                                         |
| [修改結果集資料範例](../../connect/jdbc/modifying-result-set-data-sample.md)   | 描述如何使用結果集，插入、擷取及修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料。                                                      |
| [快取結果集資料範例](../../connect/jdbc/caching-result-set-data-sample.md)       | 描述如何使用結果集，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取大量資料，以及控制如何在用戶端上快取該資料。 |
  
## <a name="see-also"></a>另請參閱

 [範例 JDBC 驅動程式應用程式](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
