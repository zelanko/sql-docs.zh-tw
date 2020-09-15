---
description: updateLong 方法 (int, long)
title: updateLong 方法 (int, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (int, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6363288-1415-4b25-8bb3-c34d6211c6d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3192996be9b61f0fb8a8e5d47cc453f36e403c73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353354"
---
# <a name="updatelong-method-int-long"></a>updateLong 方法 (int, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行索引，使用 **long** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateLong(int index,  
                       long x)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 **long** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateLong 方法是由 java.sql.ResultSet 介面中的 updateLong 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateLong 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
