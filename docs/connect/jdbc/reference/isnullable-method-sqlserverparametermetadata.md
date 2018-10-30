---
title: isNullable 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.sNullable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7e07cff-6fc4-4c9c-8e8f-838c77734bc5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d276b14fabbf815358ab56a1f0398cc183b6c2ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745655"
---
# <a name="isnullable-method-sqlserverparametermetadata"></a>isNullable 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出指定的參數中是否允許使用 Null 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int isNullable(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **int**，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 **int**，指出指定參數的可 NULL 性，可能是下列其中一個值：  
  
 ParameterMetaData.parameterNoNulls  
  
 ParameterMetaData.parameterNullable  
  
 ParameterMetaData.parameterNullabilityUnknown  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isNullable 方法是由 java.sql.ParameterMetaData 介面中的 isNullable 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
