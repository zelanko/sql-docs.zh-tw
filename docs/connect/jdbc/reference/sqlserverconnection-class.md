---
title: "SQLServerConnection 類別 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a3beda0e5629888804b522e5c4e3123e0b959ba8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnection-class"></a>SQLServerConnection 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 連接[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)、 java.io.Serializable  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>備註  
 SQLServerConnection 支援 JDBC 連接共用，而且可以是實體 JDBC 連接或邏輯 JDBC 連接。 SQLServerConnection 管理交易控制的所有陳述式所建立，而且可以參與透過 XAResource 配接器的 XA 分散式交易。  
  
 SQLServerConnection 管理已備妥的陳述式控制代碼的集區。 備妥的陳述式只需準備一次，通常就可以針對其參數使用不同的資料值來執行多次。 備妥的陳述式也會在不同的邏輯 (共用) 連接關閉之間維護。  
  
> [!NOTE]  
>  SQLServerConnection 不具備執行緒安全。 但是，從單一連接建立的多個陳述式可以同時在並行執行緒內處理。  
  
 這個類別支援解除包裝成為 SQLServerConnection 類別、 java.sql.connection 介面和 ISQLServerConnection 介面。 如需詳細資訊，請參閱[包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

