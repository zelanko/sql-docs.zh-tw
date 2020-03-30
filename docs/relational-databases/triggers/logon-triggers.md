---
title: 登入觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68058626"
---
# <a name="logon-triggers"></a>登入觸發程序
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  登入觸發程序會引發預存程序來回應 LOGON 事件。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體建立使用者工作階段時，就會引發這個事件。 登入觸發程序會在登入驗證階段結束之後，但在使用者工作階段實際建立之前引發。 因此，從觸發程序內產生且一般會顯示給使用者的所有訊息，例如錯誤訊息和來自 PRINT 陳述式的訊息，都會轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如果驗證失敗，登入觸發程序就不會引發。  
  
 您可以使用登入觸發程序稽核和控制伺服器工作階段，例如追蹤登入活動、限制登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或限制特定登入的工作階段數。 例如，在下列程式碼中，如果登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login_test *已經建立三個使用者工作階段，登入觸發程序就會拒絕該登入對* 所起始的登入嘗試。  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 請注意，LOGON 事件對應於 AUDIT_LOGIN SQL 追蹤事件，該事件可用於 [事件通知](../../relational-databases/service-broker/event-notifications.md)。 觸發程序與事件通知的主要差別在於，觸發程序會與事件同步引發，而事件通知則是非同步的。 這表示如果不要建立工作階段，就必須使用登入觸發程序。 AUDIT_LOGIN 事件的事件通知則無法這麼做。  
  
## <a name="specifying-first-and-last-trigger"></a>指定第一個和最後一個觸發程序  
 LOGON 事件可以定義多個觸發程序。 您可以使用 [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) 系統預存程序，將這些觸發程序的其中任一個指定為對事件第一個或最後一個引發的觸發程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保證其餘觸發程序的執行順序。  
  
## <a name="managing-transactions"></a>管理交易  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引發登入觸發程序之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立獨立於任何使用者交易以外的隱含交易。 因此，當第一個登入觸發程序開始引發時，交易計數為 1。 等到所有登入觸發程序完成執行之後，交易便認可。 就如同其他類型的觸發程序一樣，如果登入觸發程序完成執行時的交易計數為 0， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。 ROLLBACK TRANSACTION 陳述式會將交易計數重設為 0 (即使該陳述式是從巢狀交易內發出)。 COMMIT TRANSACTION 可能會將交易計數遞減為 0。 因此建議不要從登入觸發程序內發出 COMMIT TRANSACTION 陳述式。  
  
 在登入觸發程序內使用 ROLLBACK TRANSACTION 陳述式時，請考慮下列事項：  
  
-   一直到 ROLLBACK TRANSACTION 的時間點所做的任何資料修改都會回復。 這些修改包括目前觸發程序所做的修改，以及先前觸發程序對相同事件執行時所做的修改。 該特定事件的任何其他觸發程序則不會執行。  
  
-   目前觸發程序會繼續執行 ROLLBACK 陳述式以後出現的任何其他陳述式。 如果有任何這些陳述式修改資料，不會回復這些修改。  
  
 如果在對 LOGON 事件執行觸發程序時發生下列任一情況，不會建立使用者工作階段：  
  
-   原始隱含交易回復或失敗。  
  
-   觸發程序主體內引發嚴重性超過 20 的錯誤。  
  
## <a name="disabling-a-logon-trigger"></a>停用登入觸發程序  
 登入觸發程序可以有效地防止所有使用者成功連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，包括 **sysadmin** 固定伺服器角色的成員。 當登入觸發程序防止連接時， **sysadmin** 固定伺服器角色的成員可以使用專用管理員連接或以最低組態模式 (-f) 啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，藉以進行連接。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|Task|主題|  
|----------|-----------|  
|描述如何建立登入觸發程序。 登入觸發程序可以從任何資料庫建立，但會在伺服器層級註冊並儲存在 **master** 資料庫中。|[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)|  
|描述如何修改登入觸發程序。|[ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|描述如何刪除登入觸發程序。|[DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|描述如何傳回有關登入觸發程序的詳細資訊。|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|描述如何擷取登入觸發程序事件資料。||  
  
## <a name="see-also"></a>另請參閱  
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)  
  
  
