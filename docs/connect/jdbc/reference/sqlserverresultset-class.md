---
title: SQLServerResultSet 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e0a2185037f54aa7ed975667c0bdd5fb921c845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970610"
---
# <a name="sqlserverresultset-class"></a>SQLServerResultSet 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 結果集。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Remarks  
 結果集有兩種類型：用戶端和伺服器端。  
  
 如果結果可以納入用戶端處理序記憶體，便使用用戶端結果集。 這些結果可提供最快效能，而且可由 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 從資料庫中完整讀取。 這些結果集不會因建立伺服器端資料指標所衍生負擔而對資料庫產生額外負載。 不過，這些類型屬於不可更新的結果集。  
  
 如果結果無法納入用戶端處理序記憶體或是結果集必須為可更新狀態，就會使用伺服器端結果集。 使用這種結果集時，JDBC Driver 會建立伺服器端資料指標，並且在使用者捲動資料指標時明確提取結果集的資料列。  
  
 SQLServerResultSet 類別提供多種方法，可讓您使用任何原生 Java 資料類型和多種 Java 物件類型來更新結果集。  
  
 這個類別支援解除包裝為 SQLServerResultSet 類別、ISQLServerResultSet 介面和 sql ResultSet 介面。 如需詳細資訊, 請參閱包裝函式[和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
