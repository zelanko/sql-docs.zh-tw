---
title: createStatement 方法 (int, int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84afda93fa79d226eec21cb92c16ff5ebbc55fa5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955318"
---
# <a name="createstatement-method-int-int"></a>createStatement 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件，它會產生具有指定類型和並行的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>參數  
 *resultSetType*  
  
 表示結果集類型的 **int** 值。  
  
 *resultSetConcurrency*  
  
 表示結果集並行類型的 **int** 值。  
  
## <a name="return-value"></a>傳回值  
 語句物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 createStatement 方法是由連接介面中的 createStatement 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [createStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
