---
title: 系統相容性檢視（Transact-sql） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018029"
---
# <a name="system-compatibility-views-transact-sql"></a>系統相容性檢視（Transact-sql）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的許多系統資料表現在都當做一組檢視進行實作。 這些檢視就是所謂的相容性檢視，而且只是為了與舊版相容。 相容性檢視所公開的中繼資料與 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 提供的中繼資料相同。 然而，相容性檢視並不會公開與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中所導入之功能相關的任何中繼資料。 因此，當您使用新功能時 (例如 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 或分割)，必須改用目錄檢視。  
  
 升級為目錄檢視的另一個原因，是儲存使用者識別碼和類型識別碼的相容性檢視資料行，可能會傳回 NULL 或觸發程序算術溢位。 這是因為您可以建立超過 32,767 位使用者、群組和角色，以及 32,767 個資料類型。 例如，如果您要建立 32,768 位使用者，然後再執行下列查詢：`SELECT * FROM sys.sysusers`。 如果 ARITHABORT 設為 ON，則查詢會因為算術溢位錯誤而失敗。 如果 ARITHABORT 設定為 OFF， **uid**資料行就會傳回 Null。  
  
 為了防止上述問題發生，建議您使用可以處理逐漸遞增的使用者識別碼和類型識別碼的新目錄檢視。 下表將列出屬於這個溢位的資料行。  
  
|資料行名稱|相容性檢視|SQL Server 2005 檢視|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**uid**|**sysobjects**|**sys.objects**|  
|**uid**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**授權**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**uid**|**systypes**|**sys.types**|  
|**uid**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**uid**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**uid**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 在使用者資料庫中參考時，在 SQL Server 2000 （例如**sys.syslanguages**或**syscacheobjects**）中宣告為已被取代的系統資料表，現在已系結至**sys**架構中的後置相容性檢視。 由於 SQL Server 2000 的系統資料表已經過多個版本取代，所以此變更並非視為重大變更。  
  
 範例：如果使用者在使用者資料庫中建立名為**sys.syslanguages**的使用者資料表，在 SQL Server 2008 中，該資料庫中`SELECT * from dbo.syslanguages;`的語句會傳回使用者資料表中的值。 從 SQL Server 2012 開始，這種作法會從系統**sys.syslanguages**傳回資料。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [將系統資料表對應至系統檢視 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
