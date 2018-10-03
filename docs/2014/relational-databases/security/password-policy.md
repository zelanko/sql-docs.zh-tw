---
title: 密碼原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7b28043d797585496686dea6fd0c5fad276f16b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049979"
---
# <a name="password-policy"></a>密碼原則
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用 Windows 密碼原則機制。 密碼原則適用於使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入，以及適用於具有密碼的自主資料庫使用者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可將 Windows 所使用的相同複雜性和到期原則套用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部使用的密碼。 這項功能取決於 `NetValidatePasswordPolicy` API。  
  
## <a name="password-complexity"></a>密碼複雜性  
 密碼複雜性原則是為了阻止暴力攻擊而設計，方法是盡可能地增加密碼數目。 當強制執行密碼複雜性原則時，新的密碼必須符合下列指導方針：  
  
-   密碼不包含使用者的帳戶名稱。  
  
-   密碼長度至少為八個字元。  
  
-   密碼包含下列四種類別的其中三種：  
  
    -   拉丁文大寫字母 (A 到 Z)。  
  
    -   拉丁文小寫字母 (a 到 z)。  
  
    -   以 10 為基底的數字 (0 到 9)。  
  
    -   非英數字元，例如：驚嘆號 (!)、錢幣符號 ($)、數字符號 (#) 或百分比符號 (%)。  
  
 密碼長度最多可達 128 個字元。 您應該盡可能使用長且複雜的密碼。  
  
## <a name="password-expiration"></a>密碼過期  
 密碼過期原則用於管理密碼的壽命。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 強制執行密碼到期原則時，系統會提醒使用者變更舊密碼和停用有過期密碼的帳戶。  
  
## <a name="policy-enforcement"></a>原則強制執行  
 可個別對每一個 SQL Server 登入設定密碼原則的強制執行。 使用 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql) 來設定 SQL Server 登入的密碼原則選項。 下列規則會套用至密碼原則強制執行的組態：  
  
-   當 CHECK_POLICY 改為 ON 時，會發生下列行為：  
  
    -   CHECK_EXPIRATION 也會設為 ON，除非它已明確設為 OFF。  
  
    -   密碼記錄會使用目前密碼雜湊的值來初始化。  
  
    -   [帳戶鎖定期間]、[帳戶鎖定閾值] 和 [重設帳戶鎖定計數器的時間] 也會啟用。  
  
-   當 CHECK_POLICY 改為 OFF 時，會發生下列行為：  
  
    -   CHECK_EXPIRATION 也會設為 OFF。  
  
    -   會清除密碼記錄。  
  
    -   會重設 `lockout_time` 的值。  
  
 有些原則選項組合不受支援。  
  
-   如果指定 MUST_CHANGE，則 CHECK_EXPIRATION 和 CHECK_POLICY 必須設為 ON。 否則，陳述式便會失敗。  
  
-   如果 CHECK_POLICY 設為 OFF，CHECK_EXPIRATION 就不可設為 ON。 具有這些選項組合的 ALTER LOGIN 陳述式會失敗。  
  
 設定 CHECK_POLICY = ON 將阻止建立密碼：  
  
-   Null 或空白  
  
-   與電腦或登入名稱相同  
  
-   下列其中之一："password"、"admin"、"administrator"、"sa"、"sysadmin"  
  
 安全性原則可能是在 Windows 中設定的，也可能是從網域收到的。 若要檢視電腦上的密碼原則，請使用 [本機安全性原則] MMC 嵌入式管理單元 (**secpol.msc**)。  
  
## <a name="related-tasks"></a>相關工作  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
 [ALTER USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-user-transact-sql)  
  
 [建立登入](authentication-access/create-a-login.md)  
  
 [建立資料庫使用者](authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>相關內容  
 [增強式密碼](strong-passwords.md)  
  
  
