---
title: setNull 方法 (int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c74e06-2858-49ba-bae7-b88808e5fff4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3ed2cca1d150c89418a1ba20fc110e199c457c5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80913667"
---
# <a name="setnull-method-int-int-javalangstring"></a>setNull 方法 (int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在給定要設定之參數的類型和名稱時，將指定的參數設定為 null 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNull(int paramIndex,  
                          int sqlType,  
                          java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>參數  
 *paramIndex*  
  
 **int**，指出參數編號。  
  
 *sqlType*  
  
 JDBC 型別程式碼，如 java.sql.Types 所定義。  
  
 *typeName*  
  
 **String**，指出正在設定的參數完整名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setNull 方法是由 java.sql.PreparedStatement 介面中的 setNull 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNull 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
