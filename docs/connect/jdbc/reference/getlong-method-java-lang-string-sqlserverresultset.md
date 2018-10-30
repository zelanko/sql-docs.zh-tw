---
title: getLong 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getLong (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7bd39d61-7461-443e-a580-753d55ef6903
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06bce0f40d38ef086478d29a6f685a8bfc49ff3f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837596"
---
# <a name="getlong-method-javalangstring-sqlserverresultset"></a>getLong 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行名稱的值來當作 **long**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public long getLong(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 A**長**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getLong 方法是由 java.sql.ResultSet 介面中的 getLong 方法指定。  
  
 只有可以安全傳回整數值 (如 bigint、int、smallint、tinyint 和 bit) 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型才支援這個方法。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getLong 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
