---
title: getArray 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b839d3f-5a4e-43da-b93c-dc9e0f6d4b3b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5469eb85d3397aff2fa437a8d753c30c4b8641d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625136"
---
# <a name="getarray-method-int"></a>getArray 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的參數索引，擷取指定參數的值來作為 Array 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>參數  
 *i*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 陣列物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getArray 方法是由 java.sql.CallableStatement 介面中的 getArray 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getArray 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
