---
title: 變更伺服器驗證模式 | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a8ffafae40991d6134925481409b5898b06c20c4
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288562"
---
# <a name="change-server-authentication-mode"></a>變更伺服器驗證模式

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 變更 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的伺服器驗證模式。 在安裝期間， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會設為 **[Windows 驗證模式]** 或 **[SQL Server 及 Windows 驗證模式]** 。 安裝後，您可以隨時變更驗證模式。

如果您在安裝期間選取 [Windows 驗證模式]  ，sa 登入便會停用，且安裝程式會指派密碼。 即使稍後將驗證模式改成 [SQL Server 及 Windows 驗證模式]  ，sa 登入也會保持停用狀態。 若要使用 sa 登入，請使用 ALTER LOGIN 陳述式啟用 sa 登入並指派新密碼。 sa 登入只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到伺服器。

## <a name="before-you-begin"></a>開始之前

sa 帳戶是已知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，而且經常是惡意使用者的攻擊目標。 除非您的應用程式需要，否則請勿啟用 sa 帳戶。 請務必針對 sa 登入使用一個增強式密碼。

## <a name="change-authentication-mode-with-ssms"></a>使用 SSMS 變更驗證模式

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]  。

2. 在 **[安全性]** 頁面上的 **[伺服器驗證]** 中，選取新的伺服器驗證模式，然後按一下 **[確定]** 。

3. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊中，按一下 **[確定]** 以確認需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

4. 在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [重新啟動]  。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 正在執行，也必須將它重新啟動。

## <a name="enable-sa-login"></a>啟用 SA 登入

您可以使用 SSMS 或 T-SQL 來啟用 **SA** 登入。

### <a name="use-ssms"></a>使用 SSMS

1. 在物件總管中，依序展開 [安全性]  和 [登入]，並以滑鼠右鍵按一下 [sa]  ，然後按一下 [屬性]  。

2. 在 [一般]  頁面上，您可能必須為 **sa** 登入建立並確認密碼。

3. 在 **[狀態]** 頁面的 **[登入]** 區段中按一下 **[已啟用]** ，然後按一下 **[確定]** 。

### <a name="using-transact-sql"></a>使用 TRANSACT-SQL

下列範例會啟用 sa 登入並設定新密碼。 請先使用強式密碼取代 `<enterStrongPasswordHere>` 再執行。

```sql  
ALTER LOGIN sa ENABLE ;  
GO  
ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
GO  
```

## <a name="change-authentication-mode-t-sql"></a>變更驗證模式 (T-SQL)

下列範例會將伺服器驗證從混合模式 (Windows + SQL) 變更為只有 Windows。

> [!CAUTION]
> 下列範例會使用擴充的預存程序來修改伺服器登錄。 若未正確修改登錄，可能會發生嚴重的問題。 這些問題可能會需要您重新安裝作業系統。 Microsoft 不保證能解決這些問題。 您必須自行承擔修改登錄的風險。

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1
GO
```

## <a name="see-also"></a>另請參閱

 [增強式密碼](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md) [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md) [當系統管理員遭到鎖定時連線到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)
