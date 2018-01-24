---
title: "設定 user options 伺服器組態選項 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- global default for all users [SQL Server]
- users [SQL Server], global defaults
- user options option [SQL Server]
ms.assetid: cfed8f86-6bcf-4b90-88eb-9656e22d5dc5
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7cd2202d31fdb2b68b25bbe2214df156e38b9ce7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="configure-the-user-options-server-configuration-option"></a>設定 user options 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] user options [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **user options** 選項指定所有使用者的全域預設值。 會為使用者工作階段的持續時間建立預設查詢處理選項的清單。 **user options** 選項允許您變更 SET 選項的預設值 (如果伺服器的預設值不適當)。  
  
 使用者可以使用 SET 陳述式來覆寫這些預設值。 您可以動態設定 **user options** 以供新的登入使用。 變更 **user options**的設定之後，新的登入工作階段就會使用新的設定；目前的登入工作階段則不會受到影響。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要使用下列項目設定 user options 組態選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作**  [設定 user options 組態選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   下表列出及描述 **user options**的組態值。 不是所有組態值都彼此相容。 例如，不能同時設定 ANSI_NULL_DFLT_ON 與 ANSI_NULL_DFLT_OFF。  
  
    |ReplTest1|組態|描述|  
    |-----------|-------------------|-----------------|  
    |@shouldalert|DISABLE_DEF_CNST_CHK|控制暫時的或延遲的條件約束檢查。|  
    |2|IMPLICIT_TRANSACTIONS|如果是 dblib 網路程式庫連接，則控制執行陳述式時是否隱含地啟動交易。 IMPLICIT_TRANSACTIONS 設定在 ODBC 或 OLEDB 連接上無效。|  
    |4|CURSOR_CLOSE_ON_COMMIT|控制執行認可作業後資料指標的行為。|  
    |8|ANSI_WARNINGS|控制彙總警告中的截斷與 NULL。|  
    |16|ANSI_PADDING|控制固定長度變數的填補。|  
    |32|ANSI_NULLS|控制使用相等運算子時 NULL 的處理方式。|  
    |64|ARITHABORT|查詢執行過程中發生溢位或除以零的錯誤時終止查詢。|  
    |128|ARITHIGNORE|查詢過程中發生溢位或除以零的錯誤時傳回 NULL。|  
    |256|QUOTED_IDENTIFIER|評估運算式時區別單引號與雙引號。|  
    |512|NOCOUNT|關閉每個陳述式結束時傳回的訊息，這些訊息會說明有多少資料列受到影響。|  
    |1024|ANSI_NULL_DFLT_ON|更改工作階段的行為，使 Null 屬性與 ANSI 相容。 新定義的資料行若未明確定義 Null 屬性，就允許 Null。|  
    |2048|ANSI_NULL_DFLT_OFF|更改工作階段的行為，使 Null 屬性與 ANSI 不相容。 新定義的資料行若未明確定義 Null 屬性，則不允許 Null。|  
    |4096|CONCAT_NULL_YIELDS_NULL|將字串與 NULL 值串連時傳回 NULL。|  
    |8192|NUMERIC_ROUNDABORT|運算式中發生失去有效位數時產生錯誤。|  
    |16384|XACT_ABORT|如果 Transact- SQL 陳述式引發執行階段錯誤，就回復交易。|  
  
-   **user options** 中的位元位置與 @@OPTIONS 中的位元位置完全一樣。 每個連接都有它自己的 @@OPTIONS 函數，代表組態環境。 登入 \ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，使用者會收到將目前 **user options** 值指派給 @@OPTIONS 的預設環境。 為 **user options** 執行 SET 陳述式會影響工作階段的 @@OPTIONS 函式中的對應值。 在變更這個設定值後建立的連接都會接收新的值。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>若要設定 user options 組態選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[連接]** 節點。  
  
3.  在 **[預設連接選項]** 方塊中，選取一個或多個屬性來設定所有連接的使用者的預設查詢處理選項。  
  
     預設是無設定任何使用者選項。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>若要設定 user options 組態選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 設定 `user options` ，以變更 ANSI_WARNINGS 伺服器選項的設定值。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'user options', 8 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
##  <a name="FollowUp"></a> 後續操作：設定 user options 組態選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
