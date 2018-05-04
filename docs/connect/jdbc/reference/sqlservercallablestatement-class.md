---
title: SQLServerCallableStatement 類別 |Microsoft 文件
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
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b9942e976f1c6db89cc776f34f7639ff1c8e5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 這個類別也會提供擷取傳回狀態值的能力，其方式是使用 ? = call( ?, ..) 語法。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **擴充：** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>備註  
 SQLServerCallableStatement 可讓您指定要連同輸入和輸出參數呼叫的預存程序名稱。 SQLServerCallableStatement 也會提供擷取傳回狀態值的能力`? = call( ?, ..)`語法。  
  
 這個類別支援解除包裝成為 SQLServerCallableStatement 類別、 ISQLServerCallableStatement 介面、 java.sql.CallableStatement 介面和類別及 SQLServerPreparedStatement 所支援的解除包裝介面。 如需詳細資訊，請參閱[包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 當 SQLServerCallableStatement 的其中一個設定方法呼叫的類型，如果該型別與指定的類型衝突[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)，使用最後一個 SQLServerCallableStatement set 方法所指定之類型。 但是，這可能會導致不相容的資料類型轉換錯誤。 如果 SQLServerCallableStatement set 方法不呼叫時，第一個指定的型別[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)呼叫使用。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 驅動程式 3.0 與 JDBC 4.0 建議相容，結果集，且必須擷取更新計數，然後才能擷取 OUT 參數。 如果在結果集和更新計數完全處理完之前擷取 OUT 參數，則尚未處理的任何結果集和更新計數都會遺失。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
