---
title: "SQLServerParameterMetaData 類別 |Microsoft 文件"
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
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd97c5667d774829fb801ad22211d338afde1453
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverparametermetadata-class"></a>SQLServerParameterMetaData 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表準備陳述式參數的中繼資料。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.lang.Object  
  
 **實作：** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>備註  
 為了擷取參數中繼資料，準備好的陳述式會搭配 SET FMT ONLY 一起執行。 可呼叫的陳述式會呼叫 sp_sproc_columns 來擷取程序參數的名稱和中繼資料。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
