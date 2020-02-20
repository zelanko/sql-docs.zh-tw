---
title: getRef 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getRef (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 905dd02a-0c7f-475b-8be4-341b4359c766
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7796b766ac8593f557e64d2ebb6e324abf0ec82
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980597"
---
# <a name="getref-method-int"></a>getRef 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定的參數索引來擷取所指定參數的值作為 Ref 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Ref getRef(int i)  
```  
  
#### <a name="parameters"></a>參數  
 *i*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Ref 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getRef 方法是由 java.sql.CallableStatement 介面中的 getRef 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getRef 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
