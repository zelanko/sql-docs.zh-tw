---
title: 依照排程評估原則式管理原則 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ad7d22492411538a1f397f1a7d02436d1a02bde7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901149"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>依照排程評估原則式管理原則
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中依照排程評估原則式管理原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來依照排程評估原則：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>若要依照排程評估原則  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要評估之原則排程的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  按一下加號展開 **[原則]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要評估其排程的原則，然後選取 [屬性]  。  
  
6.  在 [開啟原則 -_policy_name_]  對話方塊的 [評估模式]  清單中，選取 [按排程時間]  。  
  
7.  在 **[排程]** 底下，按一下 **[挑選]** 指定現有的排程，或按一下 **[新增]** 建立新的排程。  
  
8.  完成後，請按一下 **[確定]** 。  
  
  
