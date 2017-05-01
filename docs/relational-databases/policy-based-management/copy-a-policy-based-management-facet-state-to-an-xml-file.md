---
title: "將原則式管理 Facet 狀態複製到 XML 檔案 | Microsoft 文件"
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
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0248d7e6090eb1a5cab319b7b41e1f2baebc98b7
ms.lasthandoff: 04/11/2017

---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>將原則式管理 Facet 狀態複製到 XML 檔案
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中將原則式管理 Facet 的狀態複製到 XML 檔案。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，將 Facet 狀態複製到 XML 檔案：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 本主題中的程序需要 msdb 資料庫的 PolicyAdministratorRole 角色成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>將 Facet 狀態複製到 XML 檔  
  
1.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體、執行個體物件、資料庫或資料庫物件，然後按一下 [Facet]。  
  
2.  在 [檢視 Facet - *object_name*] 對話方塊中，按一下 [將目前狀態匯出為原則]。  
  
3.  在 [匯出為原則] 對話方塊中，輸入檔案的路徑和名稱，或使用 [瀏覽] (**...**) 按鈕找出檔案，然後輸入 XML 檔的名稱。 如需有關此對話方塊可用之選項的詳細資訊，請參閱＜ [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md)＞。  
  
4.  完成後，請按一下 **[確定]**。  
  
  
