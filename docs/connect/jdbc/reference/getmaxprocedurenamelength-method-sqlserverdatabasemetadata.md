---
title: getMaxProcedureNameLength 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxProcedureNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1c05eb3-8465-46fd-99bc-5e8effcafee5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90bb02725131a3e770c6471a956ee02f73a293c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32835783"
---
# <a name="getmaxprocedurenamelength-method-sqlserverdatabasemetadata"></a>getMaxProcedureNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在程序名稱中使用的最大字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxProcedureNameLength()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出允許的字元數目上限。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxProcedureNameLength 方法是由 java.sql.DatabaseMetaData 介面中 getMaxProcedureNameLength 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
