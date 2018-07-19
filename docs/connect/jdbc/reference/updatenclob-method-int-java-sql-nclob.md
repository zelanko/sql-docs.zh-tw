---
title: updateNClob 方法 （int，java.sql.NClob） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6e9bca18-f64e-46a4-8541-2c9c39b393b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5861db060d978a912d973cda179cc1e878da481b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32849853"
---
# <a name="updatenclob-method-int-javasqlnclob"></a>updateNClob 方法 (int, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  更新指定的資料行與**NClob**值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.sql.NClob nClob)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *NClob*  
  
 NClob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateNClob 方法 java.sql.ResultSet 介面中所指定此 updateNClob 方法。  
  
 這個方法僅支援**nvarchar （max)**， **ntext**，和**xml**資料行。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [updateNClob 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
