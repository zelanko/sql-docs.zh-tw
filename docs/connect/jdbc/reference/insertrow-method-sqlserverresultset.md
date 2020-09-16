---
description: insertRow 方法 (SQLServerResultSet)
title: insertRow 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a399b5dbcd9d4c330c79d73b3cb2a57b2e02675
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433680"
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將插入列的內容新增到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件和資料庫中。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 insertRow 方法是由 java.sql.ResultSet 介面中的 insertRow 方法指定。  
  
 呼叫這個方法時，資料指標必須位於插入列上。 呼叫這個方法之後，資料指標仍然會在插入列上，而且結果集仍然會在插入模式下。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
