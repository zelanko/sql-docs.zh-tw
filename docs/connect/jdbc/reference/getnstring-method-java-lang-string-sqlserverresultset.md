---
title: getNString 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a76052ccf05927ebd598e2baa37fbf0229bf54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981390"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行的值來作為 java.lang.String 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 String，包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 String 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getNString 方法是由 java.sql.SQLServerResultSet 介面中的 getNString 方法指定。  
  
 這個方法可以用來抓取這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件中目前資料列內的**Nvarchar**、 **Nchar**、 **Nvarchar (max)** 、 **Ntext**或**xml**資料行的值。 如果嘗試使用這個方法來擷取其他資料類型的值，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNString 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
