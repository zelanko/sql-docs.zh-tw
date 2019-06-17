---
title: 命令語法 |Microsoft Docs
description: 命令的語法和預存程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: ac3ea02fbdf4a94f7f524022a1808410ca1dfd61
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795778"
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
  
  
