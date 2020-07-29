---
title: SQL Server Express 安全性
description: 說明 SQL Server Express 的安全性考量。
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 0e9a0b87e0275846b1c1b9535b9485dd1cbae066
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243422"
---
# <a name="sql-server-express-security"></a>SQL Server Express 安全性

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server Express Edition (SQL Server Express) 是以 Microsoft SQL Server 為基礎，可支援大部分資料庫引擎的功能。 其設計目的是要讓非必要的功能和網路連線預設為關閉。 這可減少受到惡意使用者攻擊的介面區。  
  
SQL Server Express 通常會安裝為具名執行個體。 執行個體的預設名稱為 `SQLExpress`。 具名執行個體會透過電腦的網路名稱，加上您在安裝期間所指定的執行個體名稱來識別。  
  
## <a name="network-access"></a>網路存取  
基於安全考量，在 SQL Server Express 中，依預設會停用網路通訊協定。 這可防止來自外部使用者的攻擊可能危害裝載 SQL Server Express 執行個體的電腦。 您必須明確啟用網路連線，並啟動 SQL Server Browser 服務，以便從另一部電腦連線到 SQL Server Express 執行個體。  
  
啟用網路連線之後，SQL Server Express 執行個體的安全性需求就會與其他 SQL Server 版本相同。  
  
## <a name="user-instances"></a>使用者執行個體  
使用者執行個體是 SQL Server Express 資料庫引擎的個別執行個體，其是由 SQL Server Express 的父執行個體所產生的。 使用者執行個體的主要目標是允許在最低權限使用者帳戶下執行 Windows 的使用者，在其本機電腦的 SQL Server Express 執行個體上擁有系統管理員 (`sysadmin`) 權限。 若使用者為其自己電腦上的系統管理員，則不適用使用者執行個體。  
  
使用者執行個體是代表使用者，從 SQL Server 或 SQL Server Express 的主要執行個體產生的。 它會在該使用者的 Windows 資訊安全內容下，以使用者處理序的形式執行，而非服務。 不允許 SQL Server 登入；僅支援 Windows 登入。 這可防止在使用者執行個體上執行的軟體對整個系統進行變更，而該使用者可能無權執行此作業。 使用者執行個體也稱為子系或用戶端執行個體，有時會使用 RANU 縮寫 (「以一般使用者身分執行」) 來提及。  
  
每個使用者執行個體都會與父執行個體，以及相同電腦上執行的其他使用者執行個體隔離。 安裝在使用者執行個體上的資料庫只會以單一使用者模式開啟；多個使用者無法連線到資料庫。 已針對使用者執行個體停用複寫、分散式查詢和遠端連線。 連線到使用者執行個體時，使用者在父 SQL Server Express 執行個體上沒有任何特殊權限。  
  
## <a name="external-resources"></a>外部資源  
如需 SQL Server Express 的詳細資訊，請參閱下列資源。  
  
|資源|說明|
|-|-|  
|[Microsoft SQL Server 2005 Express Edition 線上叢書](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|SQL Server 2005 Express Edition 的完整文件。|  
|《SQL Server 線上叢書》中的[非管理員的使用者執行個體](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100))|描述如何建立及部署使用者執行個體。|  
|[SQL Server Express 使用者執行個體](sql-server-express-user-instances.md)|描述 ADO.NET 應用程式中的使用者執行個體功能。 提供如何啟用使用者執行個體、使用 <xref:Microsoft.Data.SqlClient.SqlConnection> 連線到使用者執行個體、使用者執行個體存留期，以及使用者執行個體案例的相關資訊。|  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 安全性](sql-server-security.md)
- [SQL Server Express 使用者執行個體](sql-server-express-user-instances.md)
