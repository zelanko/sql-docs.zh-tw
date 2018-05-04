---
title: getBytes 方法 (java.lang.String) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bece743898f1dbdc78df7c7eec0130c65bdb278
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getbytes-method-javalangstring"></a>getBytes 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過給定的參數名稱，擷取指定之參數的值來當做位元組值的陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 陣列**位元組**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 在舊版的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，您可以使用 SQLServerCallableStatement.getBytes 來轉換位元組陣列之間的值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別**日期**，**時間**， **datetime2**，或**datetimeoffset**。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
 GetBytes 方法 java.sql.CallableStatement 介面中所指定這個 getBytes 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBytes 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
