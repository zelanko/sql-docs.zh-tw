---
title: SQLServerXAResource 類別 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 575982cd29c949203fdd667230cb8cad8d79f774
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784266"
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
  
## <a name="remarks"></a>Remarks  
 XA 交易會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 分散式交易協調器 (DTC) 來實作。 The SQLServerXAResource 類別會呼叫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 擴充 dll sqljdbc_xa.dll，此 dll 會與 DTC 接觸。 SQLServerXAResource (XA_START、XA_END、XA_PREPARE 等) 所接收的 XA 呼叫會對應到對應的 DTC 函式呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
