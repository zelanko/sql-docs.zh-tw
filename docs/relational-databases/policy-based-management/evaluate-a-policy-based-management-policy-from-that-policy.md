---
title: 根據該原則評估原則式管理原則
description: 了解如何使用 SQL Server Management Studio (SSMS)，在 SQL Server 中使用該原則來評估原則。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 28b605b52600fe9855fb9e96f9f2dbc99bbc6a20
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760535"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>根據原則式管理原則評估該原則
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用某個原則來評估該原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來評估原則：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>若要評估原則  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要評估之原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  按一下加號展開 **[原則]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要評估的原則，然後選取 [評估]  。  
  
6.  在 **[評估結果]**  對話方塊中，您可以查看原則評估的結果。 如果目標不符合此原則而且其屬性可透過原則式管理來重新設定，您可以按一下 [套用]  來強制符合原則。 如需有關 **[評估原則]** 對話方塊中之可用選項的詳細資訊，請參閱＜ [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md) ＞和＜ [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)＞。  
  
7.  完成後，請按一下 **[關閉]** 。  

