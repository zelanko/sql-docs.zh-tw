---
title: getNClob 方法 (java.lang.String) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45c77f1dfb32b08ca6618b0919671f31621ac608
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getnclob-method-javalangstring"></a>getNClob 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 JDBC 值**NCLOB**當做 NClob 物件在 Java 程式語言中的參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 ANClobobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetNClob 方法 java.sql.CallableStatement 介面中所指定此 getNClob 方法。  
  
 這個方法只支援擷取**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**參數。 對其他資料類型參數呼叫這些方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNClob 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
