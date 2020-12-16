---
title: 設定複寫快照集資料夾 (非預設連接埠)
titleSuffix: SQL Server on Linux
description: 了解如何在 Linux 上使用 SQL Server 複寫的非預設連接埠，設定快照集資料夾共用。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: ce4e17be837794382435c8a5369ef92a44a5b91a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471499"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>使用非預設連接埠來設定複寫 (SQL Server Linux)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

您可以在 Linux 執行個體上使用 SQL Server 來設定複寫，接聽使用 network.tcpport mssql-conf 設定來進行設定的任何連接埠。 如果下列條件成立，則必須在設定期間將連接埠附加至伺服器名稱：

1. 複寫設定涉及 Linux 上的 SQL Server 執行個體
2. 任何執行個體 (Windows 或 Linux) 正在接聽非預設通訊埠。 

在執行個體上執行 @@servername，即可找到執行個體的伺服器名稱。 請勿使用 IP 位址代替伺服器名稱。 使用「發行者」、「散發者」或「訂閱者」的 IP 位址可能會導致錯誤。

> [!NOTE]
> 使用非預設連接埠在 Linux 上建立 SQL Server 複寫，僅適用於 SQL Server 2019 與更高版本。

## <a name="examples"></a>範例

'Server1' 會接聽 Linux 上的連接埠 1500。 若要設定發行版本的 'Server1'，請以 `@distributor` 身分執行 `sp_adddistributor`。 例如： 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' 會接聽 Linux 上的連接埠 1500。 若要設定發行版本的發行者，請以 `@publisher` 身分執行 `sp_adddistpublisher`。 例如：

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' 會接聽 Linux 上的連接埠 6549。 若要將 'Server2' 設定為訂閱者，請以 `@subscriber` 身分執行 `sp_addsubscription`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' 會在伺服器名稱為 Server3 且執行個體名稱為 MSSQL2017 的 Windows 上接聽連接埠 6549。 若要將 'Server3' 設定為訂閱者，請以 `@subscriber` 身分執行 `sp_addsubscription`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>後續步驟

[概念：Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

