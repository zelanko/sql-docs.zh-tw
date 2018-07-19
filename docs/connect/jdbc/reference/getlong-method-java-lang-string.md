---
title: getLong 方法 (java.lang.String) |Microsoft 文件
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
- SQLServerCallableStatement.getLong (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 92e30537-5fd9-4b67-8b0f-486c6e840e03
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a2f22f105ea3e47b7965338abc6060162de7983
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834983"
---
# <a name="getlong-method-javalangstring"></a>getLong 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的值**長**在 Java 程式語言中使用給定的參數名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public long getLong(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 A**長**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetLong 方法 java.sql.CallableStatement 介面中所指定此 getLong 方法。  
  
 這個方法僅支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別，可以安全傳回整數值，例如**bigint**， **int**， **smallint**， **tinyint**，和**元**。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getLong 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
