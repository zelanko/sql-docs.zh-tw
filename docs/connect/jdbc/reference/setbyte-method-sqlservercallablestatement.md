---
title: setByte 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setByte
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0fbb03a5-61ee-4fb8-9dea-dce5cb1a367e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 102d77049a1fef17a483c6302dcb7edb324d1490
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928788"
---
# <a name="setbyte-method-sqlservercallablestatement"></a>setByte 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 **byte** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setByte(java.lang.String sCol,  
                    byte b)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *b*  
  
 **byte** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setByte 方法是由 java.sql.CallableStatement 介面中的 setByte 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
