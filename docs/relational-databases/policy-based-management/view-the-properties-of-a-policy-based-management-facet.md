---
title: 檢視原則式管理 Facet 的屬性
description: 了解如何使用 SQL Server Management Studio (SSMS) 來檢視 SQL Server 中原則式管理 Facet 的屬性。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3a5a938928817b8ffb5282b2af7d2a505b442302
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558089"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>檢視原則式管理 Facet 的屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中檢視原則式管理 Facet 的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來檢視 Facet 的屬性：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>若要檢視 Facet 的屬性  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要檢視其屬性之 Facet 的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  按一下加號展開 **[Facet]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要檢視其屬性的 Facet，然後選取 [屬性]  。 如需有關 [Facet 屬性 - **Facet 名稱**]  對話方塊中可用選項的詳細資訊，請參閱 [Facet 屬性對話方塊，一般頁面](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md)、[Facet 屬性對話方塊，相依原則頁面](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md)和 [Facet 屬性對話方塊，相依條件頁面](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md)。  
  
6.  完成後，請按一下 **[關閉]** 。  

