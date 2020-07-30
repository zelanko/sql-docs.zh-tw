---
title: 命令語法（Native Client OLE DB 提供者） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1fa327cac7eadf825ed5ef5564d6051d53a445ab
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243991"
---
# <a name="sql-server-native-client-command-syntax"></a>SQL Server Native Client 命令語法
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會辨識 DBGUID_SQL 宏指定的命令語法。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，此規範表示 ODBC SQL、ISO 和的混合物 [!INCLUDE[tsql](../../includes/tsql-md.md)] 是有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ISO 字串函數 LOWER 會執行相同的作業，因此，下列 SQL 陳述式是相當於以上所顯示之 ODBC 陳述式的 ISO：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當指定為命令的文字時，Native Client OLE DB 提供者會成功處理任一種語句的形式。  
  
## <a name="stored-procedures"></a>預存程序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命令來執行預存程式時，請使用命令文字中的 ODBC 呼叫 escape 順序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接著，Native Client OLE DB 提供者會使用的遠端程序呼叫機制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來優化命令處理。 例如，下列 ODBC SQL 陳述式是比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 形式慣用的命令文字：  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
