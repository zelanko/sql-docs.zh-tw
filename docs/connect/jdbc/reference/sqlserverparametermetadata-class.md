---
title: SQLServerParameterMetaData 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d24d63765f31f6c3218d8ed161af77298326ab7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797221"
---
# <a name="sqlserverparametermetadata-class"></a>SQLServerParameterMetaData 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表準備陳述式參數的中繼資料。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.lang.Object  
  
 **實作：** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Remarks  
 為了擷取參數中繼資料，準備好的陳述式會搭配 SET FMT ONLY 一起執行。 可呼叫的陳述式會呼叫 sp_sproc_columns 來擷取程序參數的名稱和中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
