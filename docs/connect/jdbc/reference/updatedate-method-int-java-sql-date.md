---
description: updateDate 方法 (int, java.sql.Date)
title: updateDate 方法 (int, java.sql.Date) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDate (int, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c5fb1292-a5cf-4cdd-8c4a-d1679944a6d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af27898aa87cdebcff9ffaa232e92bf4af230d47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353694"
---
# <a name="updatedate-method-int-javasqldate"></a>updateDate 方法 (int, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過給定的資料行索引，使用日期值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateDate(int index,  
                       java.sql.Date x)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 日期值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateDate 方法是由 java.sql.ResultSet 介面中的 updateDate 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateDate 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
