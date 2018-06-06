---
title: setClob 方法 （java.lang.String，java.io.Reader，long） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bc9fddea-134e-4440-ba54-a1f74bb40c46
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2fb51dba5eee7258aaacabcc87f28042897a1f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setclob-method-javalangstring-javaioreader-long"></a>setClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定之的參數設定為指定的讀取器物件指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.io.Reader value,  
            long length)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 包含參數名稱的**字串**。  
  
 *value*  
  
 讀取器物件。  
  
 *長度*  
  
 A**長**，指出資料流中的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetClob 方法 java.sql.CallableStatement 介面中所指定此 setClob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [setClob 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
