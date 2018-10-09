---
title: updateLong 方法 (java.lang.String，long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6003706-35de-42b1-8f23-899a388adb5b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 506ee458c32372154703f6174b70aee7ecfc7cae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820726"
---
# <a name="updatelong-method-javalangstring-long"></a>updateLong 方法 (java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過給定的資料行名稱，使用日期值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateLong(java.lang.String columnName,  
                       long x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
 *x*  
  
 A**長**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateLong 方法是由 java.sql.ResultSet 介面中的 updateLong 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateLong 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
