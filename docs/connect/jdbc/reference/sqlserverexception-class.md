---
title: SQLServerException 類別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd15bec08cce38405e9de8e75da9936c6742eb0a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverexception-class"></a>SQLServerException 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 SQL 陳述式執行不成功或不完整。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.SQLException  
  
 **實作：** java.io.Serializable  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>備註  
 SQLServerException 類別會處理 SQL 92 和 XOPEN 狀態碼。 這些狀態碼可以使用使用者指定的連接屬性來交換。 例外狀況會寫入任何已經指定的開啟記錄檔中。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
