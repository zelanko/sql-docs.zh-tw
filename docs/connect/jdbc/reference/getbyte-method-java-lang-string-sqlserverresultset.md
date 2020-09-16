---
description: getByte 方法 (java.lang.String) (SQLServerResultSet)
title: getByte 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getByte (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 069c68ff-442d-4104-917f-3445a3ad264a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: abbfc334796d5e0b24a9618bf6bfb08198fc8851
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437020"
---
# <a name="getbyte-method-javalangstring-sqlserverresultset"></a>getByte 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，從 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的目前資料列內擷取指定資料行名稱值來作為 **byte**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public byte getByte(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 **byte** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getByte 方法是由 java.sql.ResultSet 介面中的 getByte 方法指定。  
  
 只有可安全傳回位元組值 (如 tinyint 和 bit) 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型支援這項方法。 所有其他資料類型將會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getByte 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
