---
title: 系統相容性檢視 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
author: rothja
ms.author: jroth
ms.openlocfilehash: 466dc68da1c5cef56a7debe3953ba38956bb2993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018029"
---
# <a name="system-compatibility-views-transact-sql"></a>系統相容性檢視 & Amp;#40;transact-SQL&AMP;#41
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的許多系統資料表現在都當做一組檢視進行實作。 這些檢視就是所謂的相容性檢視，而且只是為了與舊版相容。 相容性檢視所公開的中繼資料與 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 提供的中繼資料相同。 然而，相容性檢視並不會公開與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中所導入之功能相關的任何中繼資料。 因此，當您使用新功能時 (例如 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 或分割)，必須改用目錄檢視。  
  
 升級為目錄檢視的另一個原因，是儲存使用者識別碼和類型識別碼的相容性檢視資料行，可能會傳回 NULL 或觸發程序算術溢位。 這是因為您可以建立超過 32,767 位使用者、群組和角色，以及 32,767 個資料類型。 例如，如果您要建立 32,768 位使用者，然後再執行下列查詢：`SELECT * FROM sys.sysusers`。 如果 ARITHABORT 設為 ON，則查詢會因為算術溢位錯誤而失敗。 如果 ARITHABORT 設為 OFF 時， **uid**資料行會傳回 NULL。  
  
 為了防止上述問題發生，建議您使用可以處理逐漸遞增的使用者識別碼和類型識別碼的新目錄檢視。 下表將列出屬於這個溢位的資料行。  
  
|資料行名稱|相容性檢視|SQL Server 2005 檢視|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**uid**|**sysobjects**|**sys.objects**|  
|**uid**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**grantor**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**uid**|**systypes**|**sys.types**|  
|**uid**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**uid**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**uid**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 使用者資料庫中參考時，系統資料表的已被取代 SQL Server 2000 中 (例如**syslanguages**或是**syscacheobjects**)，現在會繫結中的回溯相容性檢視**sys**結構描述。 由於 SQL Server 2000 的系統資料表已經過多個版本取代，所以此變更並非視為重大變更。  
  
 範例如果使用者建立使用者資料表稱為**syslanguages**使用者資料庫，在 SQL Server 2008 中，陳述式中`SELECT * from dbo.syslanguages;`在該資料庫會從使用者資料表傳回值。 從 SQL Server 2012 中，這種做法會傳回的資料從系統檢視**sys.syslanguages**。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
