---
title: 資料庫引擎設定-使用者實例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095874"
---
# <a name="database-engine-configuration---user-instance"></a>資料庫引擎組態 - 使用者執行個體
  使用 **[使用者執行個體]** 頁面，即可為不具管理員權限的使用者產生個別的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，並將使用者加入至管理員角色。  
  
## <a name="option"></a>選項  
 啟用使用者執行個體  
 預設值為開啟。 若要停用啟用使用者執行個體的功能，請清除該核取方塊。  
  
 使用者執行個體 (也稱為子系或用戶端執行個體) 是父執行個體 (當做服務執行的主要執行個體，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) 代表使用者所產生的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]執行個體。 使用者執行個體是在該使用者的安全性內容下，以使用者處理序的形式執行。 使用者執行個體與父執行個體和電腦上執行的其他使用者執行個體隔離。 使用者執行個體功能也稱為「以一般使用者的身分執行」(RANU)。  
  
> [!NOTE]  
>  在安裝期間布建為**系統**管理員（sysadmin）固定伺服器角色成員的登入，會布建為範本資料庫中的管理員。 除非移除，否則這些登入會是使用者執行個體上 **sysadmin** (系統管理員) 固定伺服器角色的成員。  
  
 將使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員角色  
 預設值不是開啟。 若要將目前的安裝程式使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員角色，請選取該核取方塊。  
  
 身為 BUILTIN\Administrators 成員的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 使用者並不會在連接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 時，自動加入系統管理員固定伺服器角色中。 只有已明確地加入至伺服器層級之管理員角色的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 使用者可以管理 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 Built-In\Users 群組的任何成員都可以連接至 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體，但這些成員僅具有執行資料庫工作的有限權限。 因為這個原因，所以必須在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上執行的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體中，明確地為從舊版 Windows 的 BUILTIN\Administrators 和 Built-In\Users 繼承 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]權限的使用者授與管理員權限。  
  
 若要在此安裝程式結束後，對使用者角色進行任何變更，請使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 介面區組態工具 (SQLSAC.exe)。 若要更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員角色中的使用者清單，按一下 **[新增管理員]** 連結。  
  
 請確定 [User to provision (要提供的使用者)]**** 欄位有列出其權限應該更新之使用者的 DomainName\UserName。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [可用權限] **窗格的** 執行個體清單中選取要更新的角色，然後按一下向右鍵。 若要將使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有可用執行個體及可用角色的可用角色，按一下雙重向右鍵。  
  
 若要在完成選擇時實作變更，請 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。 若要結束工具而不進行變更，按一下 **[取消]**。  
  
  
