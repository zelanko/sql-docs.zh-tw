---
title: setInt 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setInt
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5e46b129-9fe1-469f-b2e8-7ce7fb832996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b4f78d918b597d9e336feb58d512c0156eadd4e9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974156"
---
# <a name="setint-method-sqlserverpreparedstatement"></a>setInt 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 **int** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setInt(int n,  
                         int value)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **int**，指出參數編號。  
  
 *value*  
  
 **int** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setInt 方法是由 java.sql.PreparedStatement 介面中的 setInt 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
