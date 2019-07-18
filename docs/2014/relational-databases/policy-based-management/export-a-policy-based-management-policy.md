---
title: 匯出原則式管理原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dc7067432c46e1d03323ed2a32dab84ebdf72755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705331"
---
# <a name="export-a-policy-based-management-policy"></a>匯出原則式管理原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中匯出原則式管理原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目來匯出原則：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-export-a-policy"></a>若要匯出原則  
  
1.  在 [物件總管] 中，按一下加號，展開包含您想要匯出之原則式管理原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  按一下加號展開 **[原則]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要匯出的原則，然後選取 [匯出原則]  。  
  
6.  在 **[匯出原則]** 對話方塊的位址列中，輸入檔案的路徑和名稱。 或者，在對話方塊的導覽窗格中尋找適當的檔案位置，然後在 **[檔案名稱]** 方塊中輸入 XML 檔案的名稱。  
  
7.  完成後，請按一下 **[儲存]** 。  
  
  
