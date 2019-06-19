---
title: 伺服器屬性 (安全性頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: beda4797b2beeeea2bfb24a35cf052b9ac22b5eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794131"
---
# <a name="server-properties---security-page"></a>伺服器屬性 - 安全性頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此頁面來檢視或修改伺服器安全性選項。  
  
## <a name="server-authentication"></a>伺服器驗證  
 **Windows 驗證模式**  
 使用 Windows 驗證來驗證所嘗試的連接。 如果在變更安全性模式時 **sa** 密碼空白，就會提示使用者輸入 **sa** 密碼。  
  
> [!IMPORTANT]  
>  Windows 驗證比 SQL Server 驗證更安全。 可能的話，您應該使用 Windows 驗證。  
  
 **SQL Server 及 Windows 驗證模式**  
 使用混合模式驗證來確認所嘗試的連接，使其具有與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的回溯相容性。 如果在變更安全性模式時 **sa** 密碼空白，就會提示使用者輸入 **sa** 密碼。  
  
> [!NOTE]  
>  變更安全性組態需要重新啟動此服務。 將伺服器驗證變更為 SQL Server 和 Windows 驗證模式時，不會自動啟用 SA 帳戶。 若要使用 SA 帳戶，請使用 ENABLE 選項來執行 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 。  
  
## <a name="login-auditing"></a>登入稽核  
 **無**  
 關閉登入稽核。  
  
 **只限失敗的登入**  
 只限稽核不成功的登入。  
  
 **只限成功的登入**  
 只限稽核成功的登入。  
  
 **失敗和成功的登入**  
 稽核所有登入嘗試。  
  
> [!NOTE]  
>  變更稽核層級需要重新啟動此服務。  
  
## <a name="server-proxy-account"></a>伺服器 Proxy 帳戶  
 **啟用伺服器 Proxy 帳戶**  
 啟用供 **xp_cmdshell**使用的帳戶。 Proxy 帳戶允許在執行作業系統命令時模擬登入、伺服器角色以及資料庫角色。  
  
> [!CAUTION]  
>  伺服器 Proxy 帳戶所使用的登入至少應該具有執行工作所需的權限。 惡意使用者可能會使用 Proxy 帳戶過多的權限來危害系統安全性。  
  
 **Proxy 帳戶**  
 指定所使用的 Proxy 帳戶。  
  
 **密碼**  
 指定 Proxy 帳戶的密碼。  
  
## <a name="options"></a>選項。  
 **啟用 C2 稽核追蹤**  
 稽核嘗試存取陳述式和物件的所有事件，並將其記錄在 \MSSQL\Data 目錄下的檔案中 (對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設執行個體)，或是記錄在 \MSSQL$*instancename*\Data 目錄下的檔案中 (對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的具名執行個體)。 如需詳細資訊，請參閱 [C2 稽核模式伺服器組態選項](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)。  
  
 **跨資料庫擁有權鏈結**  
 選取以允許資料庫作為跨資料庫擁有權鏈結的來源或目標。 如需詳細資訊，請參閱 [跨資料庫擁有權鏈結伺服器組態選項](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
