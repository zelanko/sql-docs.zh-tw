---
title: Resource 資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd43087f302adca4f20d53e63005786736188786
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560188"
---
# <a name="resource-database"></a>Resource 資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Resource 資料庫是一個唯讀的資料庫，其中包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擁有的所有系統物件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統物件 (例如 sys.objects) 實際上會保存在 Resource 資料庫中，但邏輯上會出現在每個資料庫的 sys 結構描述中。 Resource 資料庫不包含使用者資料或使用者中繼資料。  
  
 Resource 資料庫讓升級為新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的程序變得更快且更容易。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，升級需要卸除和建立系統物件。 由於 Resource 資料庫檔案包含所有系統物件，因此現在只要將單一 Resource 資料庫檔案複製到本機伺服器即可完成升級。  
  
## <a name="physical-properties-of-resource"></a>Resource 的實體屬性  
 Resource 資料庫的實體檔案名稱為 mssqlsystemresource.mdf 和 mssqlsystemresource.ldf。 這些檔案位於 \<*磁碟機*>:\Program Files\Microsoft SQL Server\MSSQL\<版本>.\<執行個體名稱>\MSSQL\Binn\ 中，因此不應被移動。 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體只有一個相關聯的 mssqlsystemresource.mdf 檔案，而且這些執行個體不共用此檔案。  
  
> [!WARNING]  
>  升級和 Service Pack 有時會提供新的資源資料庫，其會安裝到 BINN 資料夾。 變更資源資料庫的位置不受支援，亦不建議。  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>備份與還原 Resource 資料庫  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法備份 Resource 資料庫。 您可以將 mssqlsystemresource.mdf 檔視為二進位 (.EXE) 檔案而非資料庫檔案，藉以進行以檔案為基礎或以磁碟為基礎的備份，不過您無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來還原備份。 還原 mssqlsystemresource.mdf 的備份副本只能手動完成，而且您必須小心不要使用過期或可能不安全的 Resource 資料庫來覆寫目前的資料庫。  
  
> [!IMPORTANT]  
>  還原 mssqlsystemresource.mdf 的備份後，您必須重新套用任何後續的更新。  
  
## <a name="accessing-the-resource-database"></a>存取 Resource 資料庫  
 Resource 資料庫僅能由 Microsoft 客戶支援服務 (CSS) 的專業人員修改或在他們的指示下修改。 Resource 資料庫的識別碼一律為 32767。 其他與 Resource 資料庫相關聯的重要值是版本號碼以及上次更新資料庫的時間。  
  
 **若要判斷** Resource **資料庫的版本號碼，請使用**：  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 **若要判斷** Resource **資料庫上次更新的時間，請使用**：  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **若要存取系統物件的 SQL 定義，請使用 OBJECT_DEFINITION 函數：**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>相關內容  
 [系統資料庫](../../relational-databases/databases/system-databases.md)  
  
 [資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
 [以單一使用者模式啟動 SQL Server](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
