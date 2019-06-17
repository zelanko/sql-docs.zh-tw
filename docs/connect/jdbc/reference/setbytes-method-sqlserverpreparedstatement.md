---
title: setBytes 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 52e99ef9-b786-4a14-bfc5-4162e46aafbb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 126a596b36960d883abf69e4dc852f3285a893df
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797566"
---
# <a name="setbytes-method-sqlserverpreparedstatement"></a>setBytes 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的位元組陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setBytes(int n,  
                           byte[] x)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **int**，指出參數編號。  
  
 *x*  
  
 位元組的陣列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setBytes 方法是由 java.sql.PreparedStatement 介面中的 setBytes 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
