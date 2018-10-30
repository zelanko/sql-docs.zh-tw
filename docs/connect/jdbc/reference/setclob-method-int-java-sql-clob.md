---
title: setClob 方法 （int，java.sql.Clob） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setClob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 68d49f2c-fd8d-4abb-bfdc-e7b0fbd9a9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a98e39438220dea5139f1d5df65314caf08eb086
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612076"
---
# <a name="setclob-method-int-javasqlclob"></a>setClob 方法 (int, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Clob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 **int**，指出參數編號。  
  
 *clobValue*  
  
 Clob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setClob 方法由 java.sql.PreparedStatement 介面中的 setClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 方法](../../../connect/jdbc/reference/sqlserverpreparedstatement-methods.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
