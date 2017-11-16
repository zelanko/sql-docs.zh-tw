---
title: "檢視 SQL Server Audit 記錄 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: 17285d9493a8ad4507d973f2df218915f67e63e8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="view-a-sql-server-audit-log"></a>檢視 SQL Server Audit 記錄
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 登入 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，以檢視 SQL Server 稽核記錄。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視 SQL Server 稽核記錄：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 **CONTROL SERVER** 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>若要檢視 SQL Server 稽核記錄  
  
1.  在 [物件總管] 中，展開 **[安全性]** 資料夾。  
  
2.  展開 **[稽核]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要檢視的稽核記錄，然後選取 **[檢視稽核記錄]**。 這會開啟 **[記錄檔檢視器]***server_name* 對話方塊。 如需詳細資訊，請參閱 [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
4.  完成後，請按一下 **[關閉]**。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議使用記錄檔檢視器來檢視稽核記錄檔。 不過，如果您要建立自動化的監視系統，可以使用 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 函數直接讀取稽核檔案中的資訊。 直接讀取檔案會傳回稍有不同的 (未處理的) 資料格式。 如需詳細資訊，請參閱 **sys.fn_get_audit_file** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [將 SQL Server Audit 事件寫入安全性記錄檔](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
