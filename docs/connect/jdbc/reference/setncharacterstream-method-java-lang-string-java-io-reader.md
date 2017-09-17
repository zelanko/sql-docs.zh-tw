---
title: "setNCharacterStream 方法來讀取器物件的字串 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51250ced4a6925bba1493346f48ddc6035b20005
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>setNCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定之的參數設定為指定的讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 A**字串**，指出參數名稱。  
  
 *value*  
  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetNCharacterStream 方法 java.sql.CallableStatement 介面中所指定此 setNCharacterStream 方法。  
  
 這個方法應用於**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**資料型別。  
  
## <a name="see-also"></a>另請參閱  
 [setNCharacterStream 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
