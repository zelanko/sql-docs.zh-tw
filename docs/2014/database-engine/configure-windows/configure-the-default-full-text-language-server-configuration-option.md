---
title: 設定 default full-text language 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d98194f5dead58b738c39503445923d9df49be06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62787037"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>設定 default full-text language 伺服器組態選項
  `default full-text language`本主題描述如何使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../includes/tsql-md.md)]，在中設定 server configuration 選項。 `default full-text language`選項會指定全文檢索索引的預設語言值。 語言分析會針對已全文檢索索引的所有資料執行，而且相依於資料的語言。 這個選項的預設值是伺服器使用的語言。 若為當地語系化的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式會`default full-text language`將選項設定為伺服器的語言（如果有適當的相符項存在的話）。 若 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為非當地語系化的版本時，則 `default full-text language` 選項會是英文。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 default full-text language 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定預設全文檢索語言選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   當未透過 CREATE `default full-text language`全文檢索索引或 ALTER 全文檢索索引語句中的 language **language_term**選項指定資料行的語言時，會在全文檢索索引中使用選項的值。 如果不支援預設的全文檢索語言或無法使用語言分析封裝 (Linguistic Analysis Package)，CREATE 或 ALTER 作業會失敗，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將傳回錯誤訊息，表示指定的語言無效。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   `default full-text language`選項需要 LCID 值。 如需受支援的 LCID 及其相關語言的清單，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。 例如，其他語言也可以向獨立軟體廠商取得。 如果找不到特定的語言方言，全文檢索引擎就會自動切換至主要語言。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>設定 default full-text language 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]  。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 [其他] 下方，使用 **[預設全文檢索語言]** 來指定全文檢索索引資料行的預設語言值。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>設定 default full-text language 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `default full-text` 選項的值設定為荷蘭文 (`1043`)。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-default-full-text-language-option"></a><a name="FollowUp"></a> 後續操作：設定預設全文檢索語言選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
