---
title: SQL Server Express 安全性
description: 說明 SQL Server Express 的安全性考量。
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452025"
---
# <a name="sql-server-express-security"></a>SQL Server Express 安全性

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) 是以 Microsoft SQL Server 為基礎，可支援大部分資料庫引擎的功能。 其設計目的是為了讓非必要的功能和網路連線預設為關閉。 這可減少惡意使用者攻擊的介面區。  
  
SQL Server Express 通常會安裝為已命名的實例。 執行個體的預設名稱為 `SQLExpress`。 已命名的實例是由電腦的網路名稱，加上您在安裝期間指定的實例名稱所識別。  
  
## <a name="network-access"></a>網路存取  
基於安全考量，在 SQL Server Express 中，依預設會停用網路通訊協定。 這可防止來自外部使用者的攻擊可能會危害主控 SQL Server Express 實例的電腦。 您必須明確啟用網路連線，並啟動 SQL Server Browser 服務，以便從另一部電腦連接到 SQL Server Express 實例。  
  
啟用網路連線之後，SQL Server Express 實例與其他 SQL Server 版本具有相同的安全性需求。  
  
## <a name="user-instances"></a>使用者執行個體  
使用者實例是 SQL Server Express 資料庫引擎的個別實例，由 SQL Server Express 的父實例所產生。 使用者實例的主要目標是允許在最低許可權使用者帳戶下執行 Windows 的使用者，在其本機電腦上的 SQL Server Express 實例上擁有系統管理員（`sysadmin`）許可權。 使用者實例不適用於自己電腦上系統管理員的使用者。  
  
使用者實例是從 SQL Server 的主要實例或代表使用者 SQL Server Express 而產生的。 它會在使用者的 Windows 安全性內容下以使用者進程的身分執行，而不是做為服務。 不允許 SQL Server 登入;僅支援 Windows 登入。 這可防止在使用者實例上執行的軟體進行整個系統變更，而不會讓使用者擁有許可權。 使用者實例也稱為子系或用戶端實例，有時會使用 RANU 縮寫（「以一般使用者身分執行」）來參考。  
  
每個使用者實例都與其父實例以及在相同電腦上執行的其他使用者實例隔離。 安裝在使用者實例上的資料庫只會以單一使用者模式開啟;有多個使用者無法連接到它們。 使用者實例的複寫、分散式查詢和遠端連線已停用。 當連接到使用者實例時，使用者在父系 SQL Server Express 實例上沒有任何特殊許可權。  
  
## <a name="external-resources"></a>外部資源  
如需 SQL Server Express 的詳細資訊，請參閱下列資源。  
  
|||  
|-|-|  
|[Microsoft SQL Server 2005 Express Edition 線上叢書](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|SQL Server 2005 Express Edition 的完整檔。|  
|《SQL Server 線上叢書》中的[非管理員的使用者執行個體](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100))|描述如何建立和部署使用者實例。|  
|[SQL Server Express 使用者執行個體](sql-server-express-user-instances.md)|描述 ADO.NET 應用程式中的使用者實例功能。 提供如何啟用使用者實例、使用 <xref:Microsoft.Data.SqlClient.SqlConnection>、使用者實例存留期和使用者實例等連接到使用者實例的相關資訊。|  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 安全性](sql-server-security.md)
- [SQL Server Express 使用者執行個體](sql-server-express-user-instances.md)
