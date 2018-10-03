---
title: setEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c6c76715f45521c3cbaea37a89020c6cad27b5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693986"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>setEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定特定的連接執行個體的行為。 如果此設定是第一次執行已備妥的陳述式會呼叫 sp_executesql 並不準備的陳述式，它會呼叫 sp_prepexec 並實際設定備妥的陳述式控制代碼，會發生第二次執行之後，則為 false。 遵循執行，就會呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。  
## <a name="syntax"></a>語法  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>參數  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 新值**enablePrepareOnFirstPreparedStatementCall**連接屬性。  

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 這個方法是從 JDBC 驅動程式版本 6.4 可用且向外。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
