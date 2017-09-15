---
title: "getNString 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c6a228bf0087d5af7b5f44ce2888b29d9ed73351
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getnstring-method-javalangstring"></a>getNString 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，指定**NCHAR**， **NVARCHAR**，或**LONGNVARCHAR**參數做為在 Java 程式語言的字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 A**字串**，其中包含參數名稱。  
  
## <a name="return-value"></a>傳回值  
 AStringobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetNString 方法 java.sql.CallableStatement 介面中所指定此 getNString 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getNString 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 方法](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
