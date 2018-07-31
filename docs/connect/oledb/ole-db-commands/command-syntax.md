---
title: 命令語法 |Microsoft Docs
description: 命令的語法和預存程序
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
ms.openlocfilehash: 8e7fab68cc4a945bc34c64b2b832b182c734d927
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105934"
---
# <a name="command-syntax"></a>命令語法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會識別 DBGUID_SQL 巨集所指定的命令語法。 OLE DB driver for SQL Server，此規範表示 ODBC SQL、 ISO 的混合物和[!INCLUDE[tsql](../../../includes/tsql-md.md)]是有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ISO 字串函數 LOWER 會執行相同的作業，因此，下列 SQL 陳述式是相當於以上所顯示之 ODBC 陳述式的 ISO：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 指定為命令的文字時，OLE DB Driver for SQL Server 會成功處理任一種陳述式的形式。  
  
## <a name="stored-procedures"></a>預存程序  
 使用 OLE DB Driver for SQL Server 命令執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預存程序時，請使用命令文字中的 ODBC CALL 逸出序列。 接著，OLE DB Driver for SQL Server 會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的遠端程序呼叫機制來最佳化命令處理。 例如，下列 ODBC SQL 陳述式是比 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 形式慣用的命令文字：  
  
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
  
  
