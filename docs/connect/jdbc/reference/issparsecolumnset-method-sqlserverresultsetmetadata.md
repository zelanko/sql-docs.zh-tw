---
title: isSparseColumnSet 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54fb49527b8b755a884b779bd693044ee465c544
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716866"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>isSparseColumnSet 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出結果集中的資料行是否為疏鬆資料行集。  
  
## <a name="syntax"></a>語法  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 資料行的索引 (以一為基底)。  
  
## <a name="return-value"></a>傳回值  
 若結果集中的資料行為疏鬆資料行集，即為 **true**；否則為 **false**。  
  
## <a name="remarks"></a>Remarks  
 此方法不會從資料庫中擷取資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
