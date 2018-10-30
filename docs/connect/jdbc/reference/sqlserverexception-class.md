---
title: SQLServerException 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfcc73705d04b3d3efa7515f74676b0eda120323
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680276"
---
# <a name="sqlserverexception-class"></a>SQLServerException 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 SQL 陳述式執行不成功或不完整。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.SQLException  
  
 **實作：** java.io.Serializable  
  
## <a name="syntax"></a>語法  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerException 類別會處理 SQL 92 和 XOPEN 狀態碼。 這些狀態碼可以使用使用者指定的連接屬性來交換。 例外狀況會寫入任何已經指定的開啟記錄檔中。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
