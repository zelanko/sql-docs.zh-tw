---
title: "檢視或設定遠端伺服器連線選項 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 700524e1605ef7ff871d7308ea1b4caa359081c9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>檢視或設定遠端伺服器連接選項 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視或設定伺服器層級的遠端伺服器連接選項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視或設定遠端伺服器連接選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定遠端伺服器連接選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 執行 **sp_serveroption** 需要伺服器的 ALTER ANY LINKED SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>若要檢視或設定遠端伺服器連接選項  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在 [SQL Server 屬性 - \<伺服器名稱>] 對話方塊中，按一下 [連接]。  
  
3.  檢閱 **[連接]** 頁面上的 **[遠端伺服器連接]** 設定，並視需要加以修改。  
  
4.  對遠端伺服器組的另一部伺服器重複步驟 1 到步驟 3。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-remote-server-connection-options"></a>若要檢視遠端伺服器連接選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例使用 [sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md) 傳回所有遠端伺服器的相關資訊。  
  
```tsql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>若要設定遠端伺服器連接選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何使用 [sp_serveroption](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md) 設定遠端伺服器。 範例會將對應於另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體 ( `SEATTLE3`) 的遠端伺服器，設定成定序相容於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本機執行個體。  
  
```tsql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> 待處理：設定遠端伺服器連接選項之後  
 遠端伺服器必須停止並重新啟動之後，設定才能生效。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [遠端伺服器](../../database-engine/configure-windows/remote-servers.md)   
 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
