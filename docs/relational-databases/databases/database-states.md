---
title: 資料庫狀態 | Microsoft 文件
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1aa8519092b90f34089cd2c31441b51b2b0da014
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68109695"
---
# <a name="database-states"></a>資料庫狀態
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  資料庫永遠都在特定的狀態。 例如，這些狀態包括 ONLINE、OFFLINE 或 SUSPECT。 若要驗證資料庫目前的狀態，請選取 **sys.databases** 目錄檢視中的 [state_desc](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 資料行或是在 **DATABASEPROPERTYEX** 函數中的 [Status](../../t-sql/functions/databasepropertyex-transact-sql.md) 屬性。  
  
## <a name="database-state-definitions"></a>資料庫狀態定義  
 下表定義資料表狀態。  
  
|State|定義|  
|-----------|----------------|  
|ONLINE|資料庫可供存取。 主要檔案群組是在線上，雖然可能尚未完成恢復的恢復階段。|  
|OFFLINE|資料庫是無法使用的。 明確的使用者動作可使資料庫變成離線狀態，並且在採取其他的使用者動作之前都是離線狀態。 例如，可以將資料庫設成離線，好讓檔案移到新的磁碟中。 在完成移動後，就會將資料庫重新啟動為線上狀態。|  
|RESTORING|在離線狀態還原主要檔案群組的一或多個檔案，或還原一或多個次要檔案。 資料庫是無法使用的。|  
|RECOVERING|資料庫恢復中。 恢復程序是暫時性的狀態；如果恢復成功，資料庫就會自動變成線上狀態。 如果恢復失敗，資料庫就會變成有疑問的狀態。 資料庫是無法使用的。|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在恢復期間發生資源相關的錯誤。 資料庫並未損毀，但是檔案有可能遺失或系統資源限制有可能造成它無法啟動。 資料庫是無法使用的。 需要使用者執行其他動作以解決錯誤並讓恢復處理得以完成。|  
|SUSPECT|至少主要檔案群組為有疑問的，而且有可能會損毀。 資料庫在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動期間無法恢復資料庫。 資料庫是無法使用的。 需要使用者執行其他動作來解決問題。|  
|EMERGENCY|使用者已變更資料庫並將狀態設為 EMERGENCY。 資料庫是在單一使用者模式下，而且可以進行修復或還原。 資料庫是標示為 READ_ONLY、記錄已停用並限定只有 **系統管理員** 固定伺服器角色的成員才可存取。 EMERGENCY 主要是做為疑難排解的用途。 例如，標示為有疑問的資料庫可以設為 EMERGENCY 狀態。 這將可允許系統管理員唯讀存取資料庫。 只有 **系統管理員** 固定伺服器角色的成員，可以將資料庫設定為 EMERGENCY 狀態。|  
  
## <a name="related-content"></a>相關內容  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [鏡像狀態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [檔案狀態](../../relational-databases/databases/file-states.md)  
  
  
