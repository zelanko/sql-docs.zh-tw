---
title: sys.dm_clr_properties (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f95f4d1596d84648034b51833738a26817f5e96b
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  針對與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合 (包括主控 CLR 的版本和狀態) 相關的每個屬性各傳回一個資料列。 藉由執行初始化主控的 CLR [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)， [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)，或[DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md)陳述式，或藉由執行任何 CLR 常式、 類型或觸發程序。 **Sys.dm_clr_properties**檢視不會指定是否已在伺服器上啟用使用者 CLR 程式碼的執行。 啟用使用者 CLR 程式碼的執行是利用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)預存程序與[clr 已啟用](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)選項設定為 1。  
  
 **Sys.dm_clr_properties**檢視包含**名稱**和**值**資料行。 這個檢視的每個資料列提供了有關主控 CLR 屬性的詳細資料。 請使用此檢視來收集有關主控 CLR 的資訊，例如 CLR 安裝目錄、CLR 版本，以及主控 CLR 目前的狀態。 此檢視可以幫助您判斷 CLR 整合程式碼是否因為伺服器電腦的 CLR 安裝發生問題而無法運作。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|屬性的名稱。|  
|**value**|**nvarchar(128)**|屬性的值。|  
  
## <a name="properties"></a>屬性  
 **目錄**屬性指出伺服器安裝.NET Framework 的目錄。 伺服器電腦上可能有多個 .NET Framework 安裝，而這個值可以指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在使用哪一個安裝。  
  
 **版本**屬性表示的.NET Framework 版本和伺服器上裝載 CLR。  
  
 **Sys.dm_clr_properties**動態管理的檢視可以傳回六個不同的值，如**狀態**屬性，反映出狀態[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主控 CLR。 其中包括：  
  
-   未載入 Mscoree。  
  
-   已載入 Mscoree。  
  
-   已利用 Mscoree 鎖定 CLR 版本。  
  
-   已初始化 CLR。  
  
-   CLR 初始化已永久失敗。  
  
-   CLR 已停止。  
  
 **未載入 Mscoree**和**載入 Mscoree**狀態顯示在伺服器啟動時，主控 CLR 初始化的進程，而且不可能會出現。  
  
 **利用 mscoree 鎖定 CLR 版本**其中主控的 CLR 未使用，因此，它擁有尚未初始化，可能會看到狀態。 初始化主控的 CLR 的第一次在 DDL 陳述式 (例如[CREATE ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) 或執行 managed 的資料庫物件。  
  
 **初始化 CLR**狀態表示已成功初始化主控的 CLR。 請注意，這並不會指出是否已啟用使用者 CLR 程式碼執行。 如果使用者 CLR 程式碼的執行是第一次啟用和停用使用[!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)預存程序，則狀態值仍會**初始化 CLR**。  
  
 **CLR 初始化已永久失敗**狀態指出主控 CLR 初始化失敗。 記憶體不足是可能的原因之一，或者也可能是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 之間主控交握失敗所致。 在這種情況下會發生錯誤訊息 6512 或 6513。  
  
 **CLR 已停止狀態**，才會看到當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在關閉。  
  
## <a name="remarks"></a>備註  
 屬性和值，這個檢視可能會在未來的版本中變更[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 整合功能的增強而。  
  
## <a name="permissions"></a>Permissions  
  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="examples"></a>範例  
 下列範例會擷取有關主控 CLR 的資訊：  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime 相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
