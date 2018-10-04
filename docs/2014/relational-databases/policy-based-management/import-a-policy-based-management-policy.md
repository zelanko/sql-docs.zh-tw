---
title: 匯入原則式管理原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c8be774191f0ea5e637c157be7dc95d98929ec2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175218"
---
# <a name="import-a-policy-based-management-policy"></a>匯入原則式管理原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中匯入原則式管理原則執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目來匯入原則執行個體：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附一些可用來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則。 根據預設，這些原則不會安裝在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 上，但是您可以從預設位置 C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 匯入這些原則。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>若要匯入原則執行個體  
  
1.  在物件總管中，按一下加號，展開新匯入之原則執行個體所在的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  以滑鼠右鍵按一下 [原則] 資料夾，然後選取 [匯入原則]。  
  
5.  在 [匯入] 對話方塊中，輸入檔案的路徑和名稱，或使用瀏覽 (**...**) 按鈕找出包含原則的 XML 檔案，然後選取此檔案。 如需有關 **[匯入]** 對話方塊可用之選項的詳細資訊，請參閱＜ [Import Policies Dialog Box](import-policies-dialog-box.md)＞。  
  
6.  完成後，請按一下 **[確定]**。  
  
  
