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
ms.openlocfilehash: 2cd126601c0861786ba568d9f1bc4814235b61e1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982451"
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
 **long** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getLong 方法是由 java.sql.ResultSet 介面中的 getLong 方法指定。  
  
 只有可以安全傳回整數值 (如 bigint、int、smallint、tinyint 和 bit) 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型才支援這個方法。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getLong 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
