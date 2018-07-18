---
title: getMaxCharLiteralLength 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
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
- SQLServerDatabaseMetaData.getMaxCharLiteralLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44e6e9df-4724-4c86-bbd2-ca750c248333
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d26718b8ce1b4616dfde65e9da8a019fcde5d7e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834823"
---
# <a name="getmaxcharliterallength-method-sqlserverdatabasemetadata"></a>getMaxCharLiteralLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許用於字元常值的最大字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxCharLiteralLength()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出允許的字元數目上限。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxCharLiteralLength 方法是由 java.sql.DatabaseMetaData 介面中 getMaxCharLiteralLength 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
