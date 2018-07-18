---
title: 模擬和 CLR 整合安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 05b117f27d0c27ca9288f94aade079df876fafad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243198"
---
# <a name="impersonation-and-clr-integration-security"></a>模擬和 CLR 整合安全性
  當 Managed 程式碼存取外部資源時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會自動模擬用來執行常式的目前執行內容。 `EXTERNAL_ACCESS` 和 `UNSAFE` 組件中的程式碼可以明確模擬目前的執行內容。  
  
> [!NOTE]  
>  如需模擬中行為變更的資訊，請參閱[SQL Server 2014 中的 Database Engine 功能的突破性變更](../breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 同處理序資料存取提供者會提供應用程式開發介面 `SqlContext.WindowsIdentity`，可用來擷取與目前安全性內容相關聯的 Token。 `EXTERNAL_ACCESS` 和 `UNSAFE` 組件中的 Managed 程式碼可以使用這個方法來擷取此內容並使用 .NET Framework `WindowsIdentity.Impersonate` 方法來模擬該內容。 使用者程式碼明確模擬時適用下列限制：  
  
-   當 Managed 程式碼處於模擬狀態時，不允許同處理序資料存取。 程式碼可以恢復模擬，然後呼叫同處理序資料存取。 請注意，這樣做需要儲存原始 `WindowsImpersonationContext` 方法的傳回值 (`Impersonate` 物件)，以及針對這個 `Undo` 呼叫 `WindowsImpersonationContext` 方法。  
  
     這項限制表示進行同處理序資料存取時，一定會在適用於工作階段之目前安全性內容的內容中進行， 無法由 Managed 程式碼內部的明確模擬所修改。  
  
-   若為以非同步方式執行的 Managed 程式碼 (例如，透過 `UNSAFE` 組件，建立執行緒並以非同步方式執行程式碼)，永遠不允許同處理序資料存取。 不論是否存在模擬，這項限制都成立。  
  
 執行程式碼所在的模擬內容與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不同時，它就無法執行同處理序資料存取呼叫。它應該先恢復模擬內容，然後再進行同處理序資料存取呼叫。 從 Managed 程式碼進行同處理序資料存取時，進入 Managed 程式碼之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點的原始執行內容一定會用於授權。  
  
 除非 `EXTERNAL_ACCESS` 組件和 `UNSAFE` 組件依照先前所述的方式主動模擬目前的安全性內容，否則它們會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶來存取作業系統資源。 因此，`EXTERNAL_ACCESS` 組件的作者比 `SAFE` 組件的作者需要更高的信任層級，而此信任層級是由 `EXTERNAL ACCESS` 登入層級權限所指定。 只有受信任可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶底下執行程式碼的登入才應該被授與 `EXTERNAL ACCESS` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [連接的模擬和認證](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
