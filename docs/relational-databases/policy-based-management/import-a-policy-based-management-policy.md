---
title: "匯入原則式管理原則 | Microsoft Docs"
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
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f55d3c5e57dfbd0d80e02d5c2fcb0fc6aa9ae81d
ms.lasthandoff: 04/11/2017

---
# <a name="import-a-policy-based-management-policy"></a>匯入原則式管理原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中匯入原則式管理原則執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來匯入原則執行個體：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附一些可用來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則。 依預設，這些原則不會安裝在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]上，但是您可以從預設位置 C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033 匯入這些原則。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>若要匯入原則執行個體  
  
1.  在物件總管中，按一下加號，展開新匯入之原則執行個體所在的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  以滑鼠右鍵按一下 [原則] 資料夾，然後選取 [匯入原則]。  
  
5.  在 [匯入] 對話方塊中，輸入檔案的路徑和名稱，或使用瀏覽 (**...**) 按鈕找出包含原則的 XML 檔案，然後選取此檔案。 如需有關 **[匯入]** 對話方塊可用之選項的詳細資訊，請參閱＜ [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md)＞。  
  
6.  完成後，請按一下 **[確定]**。  
  
  
