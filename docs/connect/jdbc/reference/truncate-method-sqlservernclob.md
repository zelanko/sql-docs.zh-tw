---
title: "truncate 方法 (SQLServerNClob) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8efaadf45586f631572417a364a8009d7d41e3a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="truncate-method-sqlservernclob"></a>truncate 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  會截斷**NCLOB**成指定的長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>參數  
 *len*  
  
 長度，以字元為單位，要**NCLOB**值應該會被截斷。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此截斷的方法被指定 java.sql.NClob 介面中截斷的方式。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

