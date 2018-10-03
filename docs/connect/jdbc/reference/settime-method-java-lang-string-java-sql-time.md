---
title: setTime 方法時間值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime (java.lang.String, java.lang.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49301bec-6cf2-43fb-9d4e-e3986164a208
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09cbe47839e8970954d34ecc2292faac7586136b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624976"
---
# <a name="settime-method-javalangstring-javasqltime"></a>setTime 方法 (java.lang.String, java.sql.Time)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTime(java.lang.String sCol,  
                    java.sql.Time t)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *t*  
  
 時間物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這項 setTime 方法由 java.sql.CallableStatement 介面中的 setTime 方法指定。  
  
 開頭[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]JDBC 驅動程式 3.0 中，這個方法的行為由修改**sendTimeAsDatetime**連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
