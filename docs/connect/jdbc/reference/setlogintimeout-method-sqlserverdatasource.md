---
title: setLoginTimeout 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b655449b2b15e7fbf1f31f7045bc5f0051951a2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681116"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件在嘗試建立連接時將等候的秒數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>參數  
 *loginTimeout*  
  
 **int** 值，代表要等候的秒數。 零值代表此逾時為預設系統逾時，預設指定為 15 秒。  
  
## <a name="remarks"></a>Remarks  
 SetLoginTimeout 方法由 javax.sql.DataSource 介面中所指定這個 setLoginTimeout 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
