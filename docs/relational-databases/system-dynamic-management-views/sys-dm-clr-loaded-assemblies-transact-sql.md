---
title: sys.dm_clr_loaded_assemblies (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da771a7d64383bf9328d04353c071fbe9f8a1fc6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對已載入至伺服器位址空間的每一個 Managed 使用者組件，各傳回一個資料列。 使用此檢視來了解及疑難排解 CLR 整合 managed 資料庫物件，在中執行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 組件是用來在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中定義及部署 Managed 資料庫物件的 Managed 程式碼 DLL 檔案。 每當使用者執行其中一個 Managed 資料庫物件時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 都會載入包含 Managed 資料庫物件定義的組件 (及其參考)。 為了提升效能，組件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中會保持載入的狀態，使您日後不需要重新載入組件，就可以直接呼叫包含在組件中的 Managed 資料庫物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 承受記憶體不足的壓力之前，組件都不會卸載。 如需有關組件和 CLR 整合的詳細資訊，請參閱[CLR 主控環境](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)。 如需有關 managed 的資料庫物件的詳細資訊，請參閱[建置資料庫物件與 Common Language Runtime &#40;CLR&#41;整合](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|載入組件的識別碼。 **Assembly_id**可以用來查詢中的組件的詳細資訊[sys.assemblies &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目錄檢視。 請注意， [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目錄只會在目前資料庫中顯示組件。 **Sqs.dm_clr_loaded_assemblies**檢視會顯示伺服器上所有已載入的組件。|  
|**appdomain_address**|**int**|應用程式定義域的位址 (**AppDomain**) 中的組件會載入。 單一使用者所擁有的所有組件永遠都會載入相同**AppDomain**。 **Appdomain_address**可用來查閱的詳細資訊，關於**AppDomain**中[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)檢視。|  
|**load_time**|**datetime**|載入組件的時間。 請注意，組件仍會載入直到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體不足壓力下載入和卸載**AppDomain**。 您可以監視**load_time**來了解頻率[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]承受記憶體不足的壓力而卸載**AppDomain**。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="remarks"></a>備註  
 **Dm_clr_loaded_assemblies.appdomain_address**檢視具有多對一關係**dm_clr_appdomains.appdomain_address**。 **Dm_clr_loaded_assemblies.assembly_id**檢視具有一對多關係**sys.assemblies.assembly_id**。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何檢視目前已載入現用資料庫中所有組件的詳細資料。  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 下列範例顯示如何檢視的詳細資料**AppDomain** ，其中指定的組件是已載入。  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime 相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
