---
title: isSigned 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.isSigned
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a4af386-e379-4a60-a107-a99e63a490ac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccfd2816bf81035b893ea8a7ddf30adebd325840
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796369"
---
# <a name="issigned-method-sqlserverparametermetadata"></a>isSigned 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出指定之參數的值是否可以為帶正負號的數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isSigned(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **int**，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 如果所指定參數可以包含帶正負號的數值，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isSigned 方法是由 java.sql.ParameterMetaData 介面中 isSigned 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
