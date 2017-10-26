---
title: "getBytes 方法 (SQLServerCallableStatement) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99f9e5cc54854e1406e4375b358657b3cbfde192
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值來當做位元組陣列。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|透過給定的參數索引，擷取指定之參數的值來當做位元組值的陣列。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|透過給定的參數名稱，擷取指定之參數的值來當做位元組值的陣列。|  
  
## <a name="remarks"></a>備註  
 在舊版的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，您可以使用 SQLServerCallableStatement.getBytes 來轉換位元組陣列之間的值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別**日期**，**時間**， **datetime2**，或**datetimeoffset**。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

