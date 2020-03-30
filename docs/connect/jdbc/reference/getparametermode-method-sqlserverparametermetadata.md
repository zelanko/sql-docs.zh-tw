---
title: getParameterMode 方法 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterMode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d93c9b70-18c2-44bb-a6de-70a7e940d806
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac7f8ba3b20ba8678891aeb3b14555a1123f06d1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980953"
---
# <a name="getparametermode-method-sqlserverparametermetadata"></a>getParameterMode 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getParameterMode(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **int**，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 **int**，指出指定參數的模式，可能是下列其中一個值：  
  
 ParameterMetaData.parameterModeIn  
  
 ParameterMetaData.parameterModeInOut  
  
 ParameterMetaData.parameterModeOut  
  
 ParameterMetaData.parameterModeUnknown  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getParameterMode 方法是由 java.sql.ParameterMetaData 介面中的 getParameterMode 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
