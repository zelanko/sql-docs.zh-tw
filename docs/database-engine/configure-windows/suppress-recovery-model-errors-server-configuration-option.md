---
title: 隱藏復原模式錯誤 - 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a59ff201edb153487640b4c5781d38a2df3756f9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942222"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>隱藏復原模式錯誤伺服器組態選項

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

SQL Server [復原模式](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server)可控制交易記錄維護。 完整復原模式可確保不會因為資料檔案遺失或損毀而遺失任何工作，並支援復原到備份保留原則內的任意時間點。 完整復原模式是預設值，且是 SQL 受控執行個體中唯一支援的復原模式。 嘗試在 SQL 受控執行個體中變更復原模式會傳回錯誤訊息。

使用 [隱藏復原模式錯誤] 進階組態選項，可指定在 SQL 受控執行個體上執行變更資料庫復原模式的命令時，會傳回錯誤或只傳回警告。 當此選項在 SQL 受控執行個體上設定為 1 (開啟) 時，執行 ALTER DATABASE SET RECOVERY 命令不會變更資料庫的復原模式，但仍不會傳回錯誤，而是改傳回警告訊息。 當此選項在 SQL 受控執行個體上設定為 0 (關閉) 時，執行 ALTER DATABASE SET RECOVERY 命令會傳回錯誤訊息。

在舊版或協力廠商應用程式嘗試將復原模式變更為 [簡單] 或 [大量記錄] 的情況下，[隱藏復原模式錯誤] 選項會很有幫助，但這不是重要或強制的需求。 當變更復原模式是封鎖使用 SQL 受控執行個體的唯一原因時，開啟 [隱藏復原模式錯誤] 組態選項會移除該封鎖。 如果變更應用程式程式碼的替代方案不可行或無法負擔，這個選項會特別有用。

## <a name="examples"></a>範例

下列範例可供隱藏與資料庫復原模式變更相關的錯誤訊息，然後執行命令來變更資料庫復原模式，並只傳回警告。 復原模式實際上不會變更。 請務必以實際的資料庫名稱取代 *my_database*。

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>另請參閱

[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
