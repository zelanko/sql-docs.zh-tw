---
title: SQLServerXAResource 類別 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 282201b7ff3f5b2ebfe4d8a1224d4d1b39285c53
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970089"
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 XA 分散式交易管理的 XAResource。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.lang.Object  
  
 **實作：** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>備註  
 XA 交易會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 分散式交易協調器 (DTC) 來實作。 The SQLServerXAResource 類別會呼叫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 擴充 dll sqljdbc_xa.dll，此 dll 會與 DTC 接觸。 SQLServerXAResource (XA_START、XA_END、XA_PREPARE 等) 所接收的 XA 呼叫會對應到對應的 DTC 函式呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
