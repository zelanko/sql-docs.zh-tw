---
title: updateByte 方法 (java.lang.String, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateByte (java.lang.String, byte)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5416aed2-a5b6-4e3b-9750-90db8cda8cec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ebc4d505cd116e98f5e5c68e66be7b2ea6c0274
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67996914"
---
# <a name="updatebyte-method-javalangstring-byte"></a>updateByte 方法 (java.lang.String, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行名稱，使用 **byte** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateByte(java.lang.String columnName,  
                       byte x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
 *x*  
  
 **byte** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateByte 方法是由 java.sql.ResultSet 介面中的 updateByte 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateByte 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
