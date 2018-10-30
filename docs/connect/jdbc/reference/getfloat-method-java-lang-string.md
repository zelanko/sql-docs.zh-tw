---
title: getFloat 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getFloat (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6492341-fdc2-449c-9d03-95a5dadf1bb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 471fc44de47f89438cff96ac6d3189f6224664eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711866"
---
# <a name="getfloat-method-javalangstring"></a>getFloat 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定參數名稱來擷取所指定參數的值作為 **float**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public float getFloat(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 A**浮點數**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getFloat 方法是由 java.sql.CallableStatement 介面中的 getFloat 方法指定。  
  
 這個方法會傳回所有具有 Java **float** 精確度的數字類型。  
  
## <a name="see-also"></a>另請參閱  
 [getFloat 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
