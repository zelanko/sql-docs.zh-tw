---
title: "setNCharacterStream 方法來讀取器物件-int |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5d1808b09881b314f18907941bcf98ca99ba5d4f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setncharacterstream-method-int-javaioreader"></a>setNCharacterStream 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定之的參數設定為指定的讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 **Int** ，指出參數索引。  
  
 *value*  
  
 讀取器物件，其中包含參數值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetNCharacterStream 方法 java.sql.PreparedStatement 介面中所指定此 setNCharacterStream 方法。  
  
 這個方法應用於**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**資料型別。  
  
## <a name="see-also"></a>另請參閱  
 [setNCharacterStream 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

