---
description: setMaxRows 方法 (SQLServerStatement)
title: setMaxRows 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 544eb34b40bc81afbed34809f3348c5649c3d0be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431760"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將任何 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件可以包含的最大資料列數目限制設定為所指定數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>參數  
 *max*  
  
 **int**，指出最大的資料列數目，如果沒有任何限制，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setMaxRows 方法是由 java.sql.Statement 介面中的 setMaxRows 方法指定。  
  
 這個 MaxRows 方法對動態的可捲動資料指標不會產生任何作用。 應用程式應該要使用 SELECT TOP N SQL 語法，限制可能的大型結果集傳回的資料列數。  
  
 當呼叫 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 方法時，會在其執行應用程式之查詢時執行 SET ROWCOUNT SQL 陳述式。 這將會導致 JDBC 驅動程式限制受到該查詢執行之任何 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式所影響的最大資料列數目，而非該查詢所傳回的資料列數目。 如果應用程式只需要在最上層的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件上設定限制，則它應該要在查詢中使用 SELECT TOP N SQL 語法，而不是使用 setMaxRows 方法。  
  
 如需 SET ROWCOUNT SQL 陳述式的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的 [＜SET ROWCOUNT (Transact-SQL)＞](https://go.microsoft.com/fwlink/?LinkId=139522)主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
