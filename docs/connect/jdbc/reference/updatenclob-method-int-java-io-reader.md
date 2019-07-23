---
title: updateNClob 方法 (int, java. io. 讀取器) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17adafd4-3ac3-4ff0-af9d-f087cc5ef936
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ffcdfc9249457f0371f0f400fb28e06ea02d9f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998744"
---
# <a name="updatenclob-method-int-javaioreader"></a>updateNClob 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 **Reader** 物件，更新所指定資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *reader*  
  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateNClob 方法是由 java.sql.ResultSet 介面中的 updateNClob 方法指定。  
  
 只有**Nvarchar (max)** 、 **Ntext**和**xml**資料行才支援這個方法。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [updateNClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
