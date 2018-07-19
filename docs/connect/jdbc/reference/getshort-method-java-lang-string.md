---
title: getShort 方法 (java.lang.String) |Microsoft 文件
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
- SQLServerCallableStatement.getShort (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cd39ed03-b3e8-443d-9c7a-e8cf2581e581
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d411f573d679c5f6c6040c1b3445f60d3b678b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838183"
---
# <a name="getshort-method-javalangstring"></a>getShort 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的值**簡短**在 Java 程式語言中使用給定的參數名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public short getShort(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 A**簡短**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetShort 方法 java.sql.CallableStatement 介面中所指定此 getShort 方法。  
  
 這個方法只支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以安全傳回整數值，例如 smallint、 tinyint 和 bit 資料類型。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getShort 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
