---
description: cancelRowUpdates 方法 (SQLServerResultSet)
title: cancelRowUpdates 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32e5333f571ff9375bdbdc61e9743d29a57cedfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438180"
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>cancelRowUpdates 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取消對這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列所做的更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 cancelRowUpdates 方法是由 java.sql.ResultSet 介面中的 cancelRowUpdates 方法所指定。  
  
 可以在呼叫 updater 方法之後及呼叫 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法之前呼叫這個方法，以回復之前對資料列所做的更新。 如果未做任何更新或是已經呼叫 updateRow，這個方法沒有任何作用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
