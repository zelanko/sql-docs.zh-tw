---
title: 資料庫復原模式
description: 了解如何啟用原則來檢查使用者資料庫的備份復原模式，以減少資料遺失。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 048fa8d28e32ad73aa9e2a85e217f268fa865a3c
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285073"
---
# <a name="database-recovery-model"></a>資料庫復原模式
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  針對 SQL Server Enterprise 和 Standard 版本，此規則會檢查復原設為「簡易」的非唯讀使用者資料庫。 如果是實際資料庫，我們建議您使用完整復原模式，而不要使用簡單復原模式。 完整復原模式會啟用時間點復原。 如果有損壞復原，這個模式可減少資料遺失。
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 實際資料庫應該在完整復原模式中，而且應該經常備份交易記錄來確保可復原性具有最少的資料遺失狀況。
  
## <a name="see-also"></a>另請參閱 
  
 [還原和復原概觀](../backup-restore/restore-and-recovery-overview-sql-server.md)   
  
 [完整的資料庫還原 (完整復原模式)](../backup-restore/complete-database-restores-full-recovery-model.md)  

 [交易記錄備份](../backup-restore/transaction-log-backups-sql-server.md)   
  
