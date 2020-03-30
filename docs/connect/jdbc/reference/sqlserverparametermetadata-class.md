---
title: SQLServerParameterMetaData 類別 | Microsoft Docs
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
ms.openlocfilehash: b0721341cbf095e0aa27fab392c8d03f72dc2e3a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970896"
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
  
## <a name="remarks"></a>備註  
 為了擷取參數中繼資料，準備好的陳述式會搭配 SET FMT ONLY 一起執行。 可呼叫的陳述式會呼叫 sp_sproc_columns 來擷取程序參數的名稱和中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
