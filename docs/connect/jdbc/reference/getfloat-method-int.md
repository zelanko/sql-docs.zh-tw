---
title: getFloat 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40178471-4f35-4df9-b3fb-80cdf43de274
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb0f1d7376c92eb5710e9d308d40f10fce1e3fa1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983110"
---
# <a name="getfloat-method-int"></a>getFloat 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定參數索引來擷取所指定參數值作為 **float**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public float getFloat(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 **float** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFloat 方法是由 java.sql.CallableStatement 介面中的 getFloat 方法指定。  
  
 這個方法會傳回所有具有 Java **float** 精確度的數字類型。  
  
## <a name="see-also"></a>另請參閱  
 [getFloat 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
