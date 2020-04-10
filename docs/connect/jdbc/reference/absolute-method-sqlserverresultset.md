---
title: absolute 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06a6a95838ef4ee1c605fa54fce9ef2d81f4573e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923725"
---
# <a name="absolute-method-sqlserverresultset"></a>absolute 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將資料指標移至這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的指定資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>參數  
 *row*  
  
 **int**，指出要移至的資料列編號。 可以為正數、負數或 0。  
  
## <a name="return-value"></a>傳回值  
 如果資指標移到指定位置，則為 **true**。 如果其位於第一個資料列之前或最後一個資料列之後，則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 absolute 方法是由 java.sql.ResultSet 介面中的 absolute 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
