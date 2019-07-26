---
title: deleteRow 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc02d31a1d13a3d32f581da6fb3367473cb88bbb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955131"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow 方法 (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件和基礎資料庫中，刪除目前的資料列。  
  
## <a name="syntax"></a>語法  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 deleteRow 方法是由 sql-dmo 介面中的 deleteRow 方法指定。  
  
 當資料指標位於插入資料列時，這個方法將無法進行呼叫。  
  
 當使用索引鍵集資料指標時，這個方法會在結果集中留下一個缺口。 您可以使用 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 方法來測試這個缺口。 結果集中的資料列數不會變更。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
