---
description: isFirst 方法 (SQLServerResultSet)
title: isFirst 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ff94b95-32ad-4378-8bb1-970030527bb2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 05892bce86471733edca6a19a163603dc2a6bbce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433570"
---
# <a name="isfirst-method-sqlserverresultset"></a>isFirst 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的第一個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isFirst()  
```  
  
## <a name="return-value"></a>傳回值  
 如果資料指標在第一個資料列，則為 **true**。 如果資料指標位於其他任何位置或者結果集未包含任何資料列，則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isFirst 方法是由 java.sql.ResultSet 介面中的 isFirst 方法指定。  
  
 如果搭配順向和動態資料指標使用這個方法，則會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
