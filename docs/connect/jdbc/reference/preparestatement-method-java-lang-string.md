---
title: prepareStatement 方法 (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 72b5c4a5-1382-4b2c-80a0-47c97c5f52d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8705df79119f8580d43b813dc1d9d9fcfc8c0ffd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80913938"
---
# <a name="preparestatement-method-javalangstring-int"></a>prepareStatement 方法 (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件，以便將參數化 SQL 陳述式傳送至資料庫，並且能夠傳回指定陣列所指定的自動產生索引鍵。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 包含 SQL 陳述式的**字串**。  
  
 *columnIndexes*  
  
 int 的陣列。  
  
## <a name="return-value"></a>傳回值  
 PreparedStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 prepareStatement 方法是由 java.sql.Connection 介面中的 prepareStatement 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [prepareStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
