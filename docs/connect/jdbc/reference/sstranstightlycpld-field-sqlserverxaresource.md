---
title: "SSTRANSTIGHTLYCPLD 欄位 (SQLServerXAResource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation: SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88a6ea09e8809ac028b45e2bd0fd2035b095430b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>SSTRANSTIGHTLYCPLD 欄位 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  用來允許緊密結合的 XA 交易，這些交易擁有不同的 XA 分支交易識別碼 (XID)，但是擁有相同的全域交易識別碼 (GTRID)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>欄位值  
 **Int** 32768 的值。  
  
## <a name="remarks"></a>備註  
 每一筆交易都是由 XA 分支交易識別碼 (XID) 和全域交易識別碼 (GTRID) 所識別。 為了讓應用程式使用不同的 Xid，但有相同的 GTRID 緊密結合的 XA 交易，您必須設定[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) XAResource.start 方法的旗標參數上。 如需如何使用這個旗標的詳細資訊，請參閱[了解 XA 交易](../../../connect/jdbc/understanding-xa-transactions.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerXAResource 欄位](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
