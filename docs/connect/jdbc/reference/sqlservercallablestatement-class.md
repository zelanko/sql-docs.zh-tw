---
title: SQLServerCallableStatement 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dca164af73506119cfaef376bcb7776708f76df
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783870"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 這個類別也會提供擷取傳回狀態值的能力，其方式是使用 ? = call( ?, ..) 語法。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：**[ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **擴充：**[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement 可讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 SQLServerCallableStatement 也讓您能夠擷取傳回狀態值與`? = call( ?, ..)`語法。  
  
 此類別支援解除包裝成為 SQLServerCallableStatement 類別、 ISQLServerCallableStatement 介面、 java.sql.CallableStatement 介面和類別和 SQLServerPreparedStatement 支援解除包裝的介面。 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 當 SQLServerCallableStatement 的其中一個設定方法呼叫對於類型，如果的型別與指定的類型衝突[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)，最後一個 SQLServerCallableStatement set 方法所指定之類型使用。 但是，這可能會導致不相容的資料類型轉換錯誤。 如果未呼叫 SQLServerCallableStatement set 方法，則會使用以第一個 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 呼叫所指定的類型。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 與 JDBC 4.0 建議相容，此建議中指出必須先擷取結果集和更新計數，然後才能擷取 OUT 參數。 如果在結果集和更新計數完全處理完之前擷取 OUT 參數，則尚未處理的任何結果集和更新計數都會遺失。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
