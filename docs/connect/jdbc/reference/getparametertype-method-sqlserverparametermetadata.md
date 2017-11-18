---
title: "getParameterType 方法 (SQLServerParameterMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerParameterMetaData.getParameterType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638aca05-63e4-4d73-a9c8-e0442f775720
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 37dddfba05d719af32fcb7646f05ec4be6983f7f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getparametertype-method-sqlserverparametermetadata"></a>getParameterType 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的 SQL 型別。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getParameterType(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **Int** ，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出 java.sql.Types 內定義的 JDBC 型別程式碼。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getParameterType 方法是由 java.sql.ParameterMetaData 介面中 getParameterType 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

