---
title: 命令語法 |Microsoft 文件
description: 命令語法和預存程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a3ea215d3596842503517a9485187ba2b1368059
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665748"
---
# <a name="command-syntax"></a>命令語法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server OLE DB 驅動程式會識別 DBGUID_SQL 巨集所指定的命令語法。 OLE DB driver for SQL Server，此規範表示 ODBC SQL、 ISO 的混合物和[!INCLUDE[tsql](../../../includes/tsql-md.md)]是有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ISO 字串函數 LOWER 會執行相同的作業，因此，下列 SQL 陳述式是相當於以上所顯示之 ODBC 陳述式的 ISO：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 SQL Server OLE DB 驅動程式會處理任一種陳述式成功時指定為命令的文字形式。  
  
## <a name="stored-procedures"></a>預存程序  
 執行時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]預存程序使用 OLE DB 驅動程式的 SQL Server 命令，命令文字中使用 ODBC CALL 逸出序列。 SQL Server OLE DB 驅動程式，然後使用的遠端程序呼叫機制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]來最佳化命令處理。 例如，下列 ODBC SQL 陳述式是比 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 形式慣用的命令文字：  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
