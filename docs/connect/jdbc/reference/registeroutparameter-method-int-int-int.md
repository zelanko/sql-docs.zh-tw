---
title: registerOutParameter 方法 (int, int, int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d902d4e0-881f-4182-814c-0ede9a8da7fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6948bf6b86160b1752a483b13f83abbfc467ef2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975938"
---
# <a name="registeroutparameter-method-int-int-int"></a>registerOutParameter 方法 (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在給定 JDBC 型別和小數位數的指定序數位置中註冊 OUT 參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 **int**，指出參數的序數位置。  
  
 *sqlType*  
  
 JDBC 型別程式碼，如 java.sql.Types 中所定義。  
  
 *scale*  
  
 **int**，指出位於小數點右邊的位數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 registerOutParameter 方法是由 JAVA.sql.callablestatement 介面中的 registerOutParameter 方法指定。  
  
 從 JDBC Driver 3.0 開始, 當*sqlType*的類型為**sendTimeAsDatetime**時, 這個方法的行為會由連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊, 請參閱設定將[java. Time 值傳送至伺服器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [registerOutParameter 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
