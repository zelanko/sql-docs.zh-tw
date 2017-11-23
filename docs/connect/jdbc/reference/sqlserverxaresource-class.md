---
title: "SQLServerXAResource 類別 |Microsoft 文件"
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
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ba5dd0fdce9b26e56cc9a009e901cc5d3dd46c6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XAResource 代表 xa 分散式交易管理。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.lang.Object  
  
 **實作：** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>備註  
 XA 交易中實作[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用[!INCLUDE[msCoName](../../../includes/msconame_md.md)]分散式交易協調器 (DTC)。 SQLServerXAResource 類別會呼叫[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]擴充 dll sqljdbc_xa.dll，此介面為 DTC。 SQLServerXAResource （XA_START、 XA_END、 XA_PREPARE 等等） 所接收的 XA 呼叫會對應到對應的 DTC 函數呼叫。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
