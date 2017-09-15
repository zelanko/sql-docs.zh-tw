---
title: "getNCharacterStream 方法 (int) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6ae704f5-823c-4dfe-8c08-07b547c61a3c
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1e775e27a3701581d8bf134658da439a2fbaa0b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getncharacterstream-method-int"></a>getNCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值為給定的參數索引讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.io.Reader getNCharacterStream(int parameterIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 **Int** ，指出參數索引。  
  
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
  
  
