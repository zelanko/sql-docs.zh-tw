---
title: 刪除原則式管理條件 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, delete policy conditions
ms.assetid: e04148b8-f6dd-4c50-a5ef-c650b71dbf4d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c3085a6ab63278803523e383104ab6cfb9554833
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137893"
---
# <a name="delete-a-policy-based-management-condition"></a>刪除原則式管理條件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中刪除原則式管理條件。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來刪除條件：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-condition"></a>若要刪除條件  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要刪除之條件的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  按一下加號展開 **[條件]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要刪除的條件，然後選取 [刪除]  。  
  
6.  在 **[刪除物件]** 對話方塊中，確定已選取正確的條件，然後按一下 **[確定]** 。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

