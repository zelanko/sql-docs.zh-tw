---
title: sys.databases dm_clr_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a61484691e4e5a2ea5ca4c08b6382b501f1cc851
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091857"
---
# <a name="sysdm_clr_properties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  針對與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合 (包括主控 CLR 的版本和狀態) 相關的每個屬性各傳回一個資料列。 裝載的 CLR 是藉由執行[CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)、 [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)或[DROP assembly](../../t-sql/statements/drop-assembly-transact-sql.md)語句來初始化，或是藉由執行任何 CLR 常式、類型或觸發程式來初始化。 [ **Dm_clr_properties** ] 視圖不會指定是否已在伺服器上啟用使用者 clr 程式碼的執行。 使用者 CLR 程式碼的執行會藉由使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)預存程式來啟用，並將[CLR enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)選項設定為1。  
  
 [ **Sys.databases dm_clr_properties** ] 視圖包含 [**名稱**] 和 [**值**] 資料行。 這個檢視的每個資料列提供了有關主控 CLR 屬性的詳細資料。 請使用此檢視來收集有關主控 CLR 的資訊，例如 CLR 安裝目錄、CLR 版本，以及主控 CLR 目前的狀態。 此檢視可以幫助您判斷 CLR 整合程式碼是否因為伺服器電腦的 CLR 安裝發生問題而無法運作。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|屬性的名稱。|  
|**value**|**nvarchar(128)**|屬性的值。|  
  
## <a name="properties"></a>屬性  
 **Directory**屬性會指出 .NET Framework 安裝在伺服器上的目錄。 伺服器電腦上可能有多個 .NET Framework 安裝，而這個值可以指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在使用哪一個安裝。  
  
 **Version**屬性會指出伺服器上的 .NET Framework 版本和主控的 CLR。  
  
 **Dm_clr_properties**動態受控視圖可以針對**state**屬性傳回六個不同的值，這會反映 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主控 clr 的狀態。 其中包括：  
  
-   未載入 Mscoree。  
  
-   已載入 Mscoree。  
  
-   已利用 Mscoree 鎖定 CLR 版本。  
  
-   已初始化 CLR。  
  
-   CLR 初始化已永久失敗。  
  
-   CLR 已停止。  
  
 [ **Mscoree.dll 未載入**] 和 [ **mscoree.dll 已載入**] 狀態會顯示裝載的 CLR 初始化在伺服器啟動時的進展，而且不可能出現。  
  
 在未使用託管 CLR 的情況下，可能會看到具有 mscoree.dll 狀態的已**鎖定 CLR 版本**，因此尚未初始化。 主控的 CLR 會在第一次執行 DDL 語句（例如[CREATE ASSEMBLY &#40;transact-sql&#41;](../../t-sql/statements/create-assembly-transact-sql.md)）或 managed 資料庫物件時初始化。  
  
 **CLR 已初始化**狀態表示已成功初始化主控的 CLR。 請注意，這並不會指出是否已啟用使用者 CLR 程式碼執行。 如果第一次啟用使用者 CLR 程式碼，然後使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)預存程式加以停用，則狀態值仍然會**初始化 CLR**。  
  
 **Clr 初始化永久失敗**狀態表示託管 CLR 初始化失敗。 記憶體不足是可能的原因之一，或者也可能是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 之間主控交握失敗所致。 在這種情況下會發生錯誤訊息 6512 或 6513。  
  
 **CLR 已停止狀態**，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在正在關閉的進程中才會看到。  
  
## <a name="remarks"></a>備註  
 這個視圖的屬性和值在未來的版本中可能會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 因為 CLR 整合功能的增強而變更。  
  
## <a name="permissions"></a>權限  
  
在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="examples"></a>範例  
 下列範例會擷取有關主控 CLR 的資訊：  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime 相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
