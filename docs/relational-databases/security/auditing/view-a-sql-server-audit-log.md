---
title: 檢視 SQL Server Audit 記錄 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1b1f2528b4dd6c247c37f7c1d33b91ce32b52366
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="view-a-sql-server-audit-log"></a>檢視 SQL Server Audit 記錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 登入 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，以檢視 SQL Server 稽核記錄。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目檢視 SQL Server 稽核記錄：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 **CONTROL SERVER** 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>若要檢視 SQL Server 稽核記錄  
  
1.  在 [物件總管] 中，展開 **[安全性]** 資料夾。  
  
2.  展開 **[稽核]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要檢視的稽核記錄，然後選取 **[檢視稽核記錄]**。 這會開啟 [記錄檔檢視器 –*server_name*]**** 對話方塊。 如需詳細資訊，請參閱 [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
4.  完成後，請按一下 **[關閉]**。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議使用記錄檔檢視器來檢視稽核記錄檔。 不過，如果您要建立自動化的監視系統，可以使用 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 函數直接讀取稽核檔案中的資訊。 直接讀取檔案會傳回稍有不同的 (未處理的) 資料格式。 如需詳細資訊，請參閱 **sys.fn_get_audit_file** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [將 SQL Server Audit 事件寫入安全性記錄檔](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
