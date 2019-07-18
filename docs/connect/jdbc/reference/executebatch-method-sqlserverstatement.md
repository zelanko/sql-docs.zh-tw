---
title: executeBatch 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb034f63-2532-4da8-a1b0-bc125734585a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9a4a93ccd16fccd90db0a5bb5e4e234ea3a939a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802301"
---
# <a name="executebatch-method-sqlserverstatement"></a>executeBatch 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將命令批次提交到要執行的資料庫。 如果所有命令都成功執行，則傳回更新計數陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>傳回值  
 包含更新計數的 **int** 陣列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Remarks  
 這個 executeBatch 方法是由 java.sql.Statement 介面中的 executeBatch 方法指定。  
  
 將命令提交到資料庫以後，這個方法會清除批次中的任何命令。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
