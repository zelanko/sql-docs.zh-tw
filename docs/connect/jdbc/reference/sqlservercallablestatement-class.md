---
title: SQLServerCallableStatement 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637b56c7f64d35501be0efef30e8f2a055b5be4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971910"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 這個類別也會提供擷取傳回狀態值的能力，其方式是使用 ? = call( ?, ..) 語法。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **擴充：** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement 可讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 SQLServerCallableStatement 也提供以`? = call( ?, ..)`語法抓取傳回狀態值的能力。  
  
 這個類別支援解除包裝為 SQLServerCallableStatement 類別、ISQLServerCallableStatement 介面、JAVA.sql.callablestatement 介面, 以及 SQLServerPreparedStatement 所支援的類別和介面來解除包裝。 如需詳細資訊, 請參閱包裝函式[和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 針對某個型別呼叫其中一個 SQLServerCallableStatement set 方法時, 如果該型別與使用[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)所指定的型別相衝突, 則會使用最後一個 SQLServerCallableStatement set 方法所指定的型別。 但是，這可能會導致不相容的資料類型轉換錯誤。 如果未呼叫 SQLServerCallableStatement set 方法，則會使用以第一個 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 呼叫所指定的類型。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 與 JDBC 4.0 建議相容，此建議中指出必須先擷取結果集和更新計數，然後才能擷取 OUT 參數。 如果在結果集和更新計數完全處理完之前擷取 OUT 參數，則尚未處理的任何結果集和更新計數都會遺失。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
