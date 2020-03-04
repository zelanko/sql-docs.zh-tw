---
title: SQLServerCallableStatement 類別 | Microsoft Docs
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
ms.openlocfilehash: f47c034a720be5409d83868a7a61dd229ab70e24
ms.sourcegitcommit: 92b2e3cf058e6b1e9484e155d2cc28ed2a0b7a8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/25/2020
ms.locfileid: "77600134"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 這個類別也會提供擷取傳回狀態值的能力，其方式是使用 `? = call( ?, ..)` 語法。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **擴充：** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>備註  
 SQLServerCallableStatement 可讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。 SQLServerCallableStatement 也會提供使用 `? = call( ?, ..)` 語法來擷取傳回狀態值的能力。  
  
 這個類別支援解除包裝為 SQLServerCallableStatement 類別、ISQLServerCallableStatement 介面、java.sql.CallableStatement 介面，以及 SQLServerPreparedStatement 支援來解除包裝的類別和介面。 如需詳細資訊，請參閱[包裝函式與介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 針對某個類型呼叫其中一個 SQLServerCallableStatement set 方法時，如果該類型與使用 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 指定的類型相衝突，則會使用最後一個 SQLServerCallableStatement set 方法所指定的類型。 但是，這可能會導致不相容的資料類型轉換錯誤。 如果未呼叫 SQLServerCallableStatement set 方法，則會使用以第一個 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 呼叫所指定的類型。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 與 JDBC 4.0 建議相容，此建議中指出必須先擷取結果集和更新計數，然後才能擷取 OUT 參數。 如果在結果集和更新計數完全處理完之前擷取 OUT 參數，則尚未處理的任何結果集和更新計數都會遺失。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
