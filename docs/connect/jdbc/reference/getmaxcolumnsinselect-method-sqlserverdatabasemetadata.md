---
title: getMaxColumnsInSelect 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c428df-ef91-4f55-81c3-49a4db3379cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5972396f79866a348ba004f75de3869781f418c1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907101"
---
# <a name="getmaxcolumnsinselect-method-sqlserverdatabasemetadata"></a>getMaxColumnsInSelect 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在 SELECT 清單中使用的最大資料行數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxColumnsInSelect()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大資料行數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxColumnsInSelect 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxColumnsInSelect 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
