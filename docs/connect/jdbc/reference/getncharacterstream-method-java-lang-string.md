---
title: "getNCharacterStream 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 58012af7ac3fe73f07cefc7a65fc97f89a858dc0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值為給定的參數名稱的讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 A**字串**，其中包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 AReaderobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個方法應該用來存取**NCHAR**， **NVARCHAR**和**LONGNVARCHAR**參數。  
  
 GetNCharacterStream 方法 java.sql.CallableStatement 介面中所指定此 getNCharacterStream 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
