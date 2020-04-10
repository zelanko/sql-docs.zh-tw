---
title: getPrecision 方法 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dbca77be55cd855f2e293324d6cd7c4ca5471b7e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925220"
---
# <a name="getprecision-method-sqlserverparametermetadata"></a>getPrecision 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的小數位數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **int**，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 **int**，指出指定參數的有效位數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getPrecision 方法是由 java.sql.ParameterMetaData 介面中的 getPrecision 方法所指定。  
  
 如果是數字型別，這個方法會取得小數位數。 如果是字元型別，它會取得以字元為單位的最大長度。 如果是二進位型別，它會取得以位元組為單位的最大長度。 當位數未知時，這個方法會傳回 "0"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
