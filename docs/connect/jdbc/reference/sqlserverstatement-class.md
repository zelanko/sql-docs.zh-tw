---
title: SQLServerStatement 類別 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c749554d3f95ca873c9bee61b8f6c748ccbf7906
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926998"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 陳述式功能的基本實作。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>備註  
 SQLServerStatement 類別也針對 JDBC 備妥及可呼叫的陳述式提供許多基底類別實作方法。 SQLServerStatement 類別的基本角色是執行 SQL 陳述式，然後將更新計數和結果集傳回給使用者應用程式。  
  
 這個類別支援解除包裝為 SQLServerStatement 類別、ISQLServerStatement 介面和 java.sql.Statement 介面。 如需詳細資訊，請參閱[包裝函式與介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
