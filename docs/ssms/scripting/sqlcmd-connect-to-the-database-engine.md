---
title: 使用 sqlcmd 連接至 Database Engine
description: 了解如何選取 sqlcmd 用以與 SQL Server 通訊的通訊協定。 選項有：TCP/IP、具名管道與共用記憶體。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9cf769ae3dc43e6e8c0601d25322627d7dec4920
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466229"
---
# <a name="sqlcmd---connect-to-the-database-engine"></a>sqlcmd - 連接至 Database Engine
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 TCP/IP 網路通訊協定 (預設值) 和具名管道通訊協定，來進行用戶端通訊。 如果用戶端是連接到同一部電腦上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，也可以使用共用記憶體通訊協定。 選取通訊協定有三種常見的方法。 **sqlcmd** 公用程式所使用的通訊協定是以下列順序決定：  
  
-   **sqlcmd** 使用指定為連接字串一部分的通訊協定，如下所述。  
  
-   如果沒有任何通訊協定指定為連接字串的一部分，則 **sqlcmd** 會使用定義為所連接之別名一部分的通訊協定。 若要設定 **sqlcmd** 透過建立別名來使用特定的網路通訊協定，請參閱 [建立或刪除用戶端使用的伺服器別名 #40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)。  
  
-   如果未使用其他方法指定通訊協定，則 **sqlcmd** 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中通訊協定順序所判斷的網路通訊協定。  
  
 下列範例顯示各種不同的方法，用以連接到通訊埠 1433 的預設 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，以及假設要接聽通訊埠 1691 的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 具名執行個體。 其中一部分範例使用回送網路卡的 IP 位址 (127.0.0.1)。 請使用您電腦網路介面卡的 IP 位址進行測試。  
  
 指定執行個體名稱，以連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 指定 IP 位址，以連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 指定 TCP\IP 通訊埠編號，以連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>若要使用 TCP/IP 連接  
  
-   使用下列常見語法進行連接：  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   連接到預設執行個體：  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   連接到具名執行個體：  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>若要使用具名管道連接  
  
-   使用下列一般語法的其中之一連接：  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   連接到預設執行個體：  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   連接到具名執行個體：  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>若要使用伺服器上用戶端的共用記憶體 (本機程序呼叫) 連接  
  
-   使用下列一般語法的其中之一連接：  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   連接到預設執行個體：  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   連接到具名執行個體：  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
