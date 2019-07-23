---
title: getClob 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getClob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34858e03-5b93-40b1-bf21-13ad7cc7a55e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8c2a617bb0494529254b54d81b0572f13d8b597e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953041"
---
# <a name="getclob-method-int"></a>getClob 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定的參數索引來擷取所指定 JDBC BLOB 參數值作為 Clob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Clob getClob(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Clob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getClob 方法是由 java.sql.CallableStatement 介面中的 getClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
