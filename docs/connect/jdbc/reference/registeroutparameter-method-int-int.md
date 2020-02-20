---
title: registerOutParameter 方法 (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 169229c7-b75d-498b-a5ac-df300424c909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44c9ab796c6ac0bf0d3cd48429a22d9275c01bfa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975990"
---
# <a name="registeroutparameter-method-int-int"></a>registerOutParameter 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在給定 JDBC 型別的指定序數位置中註冊 OUT 參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 **int**，指出參數的序數位置。  
  
 *sqlType*  
  
 JDBC 型別程式碼，如 java.sql.Types 中所定義。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 registerOutParameter 方法是由 java.sql.CallableStatement 介面中的 registerOutParameter 方法指定。  
  
 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 開始，當 *sqlType* 是 java.sql.Types.TIME 類型時，這個方法的行為是由 **sendTimeAsDatetime** 連線屬性 ([設定連線屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 所修改。  
  
 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [registerOutParameter 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
