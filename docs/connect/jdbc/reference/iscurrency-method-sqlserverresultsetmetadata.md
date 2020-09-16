---
description: isCurrency 方法 (SQLServerResultSetMetaData)
title: isCurrency 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7fe25d90-693c-4d3b-9dd2-0f8351c5a9ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b5c127dab64cfd77599fb9f2dfb50b4605c64e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433660"
---
# <a name="iscurrency-method-sqlserverresultsetmetadata"></a>isCurrency 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出指定的資料行是否為貨幣 (cash) 類型值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isCurrency(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 如果資料行為貨幣值，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isCurrency 方法是由 java.sql.ResultSetMetaData 介面中的 isCurrency 方法所指定。  
  
 這個方法將會傳回 **true**，其中只包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] money 和 smallmoney 資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
