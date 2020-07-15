---
title: Database Mail XPs 伺服器組態選項 | Microsoft Docs
description: 了解 [DatabaseMail XPs] 選項。 檢視開啟此選項的不同方式，以使用 SQL Server 中的 Database Mail。
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0d495017b9bf2a5f58a5a880f1ce9696976ebd50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772562"
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XP 伺服器組態選項

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

使用 [DatabaseMail XP] 選項，可在此伺服器上啟用 Database Mail。 可能的值包括：  
  
- `0`:無法使用 Database Mail (預設值)。  
  
- `1`:可以使用 Database Mail。  
  
 設定立即生效，伺服器不必停止再重新啟動。  
  
 啟用 Database Mail 後，您必須設定 Database Mail 主機資料庫來使用 Database Mail。  
  
 使用 [Database Mail 設定精靈] 設定 Database Mail，可啟用 `msdb` 資料庫中的 Database Mail 擴充預存程序。 如果您使用 [Database Mail 設定精靈]，就不需使用以下的 `sp_configure` 範例。  
  
 將 [Database Mail XP] 選項設為 `0`，會使 Database Mail 無法啟動。 如果 Database Mail 在該選項設為 `0` 時仍在執行中，則會繼續執行並傳送郵件，直到 `DatabaseMailExeMinimumLifeTime` 選項所設定的時間才會閒置。  
  
## <a name="examples"></a>範例
 下列範例會啟用 Database Mail 擴充預存程序。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  

下列範例會啟用 Database Mail 擴充預存程序 (如果尚未啟用)。

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## <a name="see-also"></a>另請參閱
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
