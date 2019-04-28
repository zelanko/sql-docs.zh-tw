---
title: 根據物件評估原則式管理原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43116e7fdec059f822a5381696a485aba767402b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62705234"
---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>根據物件評估原則式管理原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中根據伺服器執行個體、資料庫或資料庫物件評估原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目來根據物件評估原則：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   執行模式會定義成原則的一部分，而且無法在 **[評估原則]** 對話方塊中變更。  
  
-   **[評估原則]** 對話方塊只會顯示適用於資料庫物件的原則。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>若要根據物件評估原則  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器執行個體、資料庫或資料庫物件、指向 [原則]，然後選取 [評估]。  
  
2.  在 **[評估原則]** 對話方塊中，選取一個或多個原則，然後按一下 **[評估]** 以評估模式執行原則。 這樣會產生目標集的符合報表，但是不會重新設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或是強制未來的符合。 如果目標不符合選定原則而且其屬性可透過原則式管理來重新設定，您可以按一下 [套用] 來強制符合原則。 如需有關 **[評估原則]** 對話方塊可用之選項的詳細資訊，請參閱＜ [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md)＞、＜ [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)＞和＜ [Results Detailed View Dialog Box](results-detailed-view-dialog-box.md)＞。  
  
3.  完成後，請按一下 **[關閉]**。  
  
  
