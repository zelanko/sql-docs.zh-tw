---
title: Database Mail XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e916fe3b76abfa8773a757cf2779e7d5cbf26b86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810540"
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XP 伺服器組態選項
  使用 [DatabaseMail XP] 選項，可在此伺服器上啟用 Database Mail。 可能值為：  
  
-   **0** 表示無法使用 Database Mail (預設值)。  
  
-   **1** 表示可使用 Database Mail。  
  
 設定立即生效，伺服器不必停止再重新啟動。  
  
 啟用 Database Mail 後，您必須設定 Database Mail 主機資料庫來使用 Database Mail。  
  
 使用 [Database Mail 組態精靈] 設定 Database Mail，可啟用 **msdb** 資料庫中的 Database Mail 擴充預存程序。 如果您使用 [Database Mail 組態精靈]，就不需使用以下的 **sp_configure** 範例。  
  
 將 [Database Mail XP] 選項設為 0，會使 Database Mail 無法啟動。 如果 Database Mail 在該選項設為 0 時仍在執行中，則會繼續執行並傳送郵件，直到 **DatabaseMailExeMinimumLifeTime** 選項所設定的時間才會閒置。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
