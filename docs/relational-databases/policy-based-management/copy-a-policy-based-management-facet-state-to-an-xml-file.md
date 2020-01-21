---
title: 將原則式管理 Facet 狀態複製到 XML 檔案
description: 描述如何使用 SQL Server Management Studio (SSMS)，將原則式管理 Facet 的狀態複製到 XML 檔案。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fa0ee70601b11af3341483aff177ef6a7a389ba6
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558186"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>將原則式管理 Facet 狀態複製到 XML 檔案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中將原則式管理 Facet 的狀態複製到 XML 檔案。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，將 Facet 狀態複製到 XML 檔案：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 本主題中的程序需要 msdb 資料庫的 PolicyAdministratorRole 角色成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>將 Facet 狀態複製到 XML 檔  
  
1.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體、執行個體物件、資料庫或資料庫物件，然後按一下 [Facet]  。  
  
2.  在 [檢視 Facet - _物件名稱_]  對話方塊中，按一下 [將目前狀態匯出為原則]  。  
  
3.  在 [匯出為原則] 對話方塊中，輸入檔案的路徑和名稱，或使用 [瀏覽] \(...) 按鈕找出檔案，然後輸入 XML 檔的名稱。   如需有關此對話方塊可用之選項的詳細資訊，請參閱＜ [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md)＞。  
  
4.  完成後，請按一下 **[確定]** 。  
  
  
