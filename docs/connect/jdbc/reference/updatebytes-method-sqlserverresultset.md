---
title: updateBytes 方法 (SQLServerResultSet) |Microsoft 文件
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
- SQLServerResultSet.updateBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3050c836-fbb3-4475-99e5-05637a48a932
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a01c403fee7f0619009d53dd4376ee9d4e6d728
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updatebytes-method-sqlserverresultset"></a>updateBytes 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  更新指定的資料行的陣列**位元組**值。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|Description|  
|----------|-----------------|  
|[updateBytes (int，位元組&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-int-byte.md)|更新指定的資料行的陣列**位元組**給定的資料行索引的值。|  
|[updateBytes (java.lang.String，byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-java-lang-string-byte.md)|更新指定的資料行的陣列**位元組**給定的資料行名稱的值。|  
  
## <a name="remarks"></a>備註  
 在舊版的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，您可以使用 SQLServerResultSet.updateBytes 來轉換位元組陣列之間的值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別**日期**，**時間**， **datetime2**，或**datetimeoffset**。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
