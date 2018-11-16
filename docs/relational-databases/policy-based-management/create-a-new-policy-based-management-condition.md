---
title: 建立新的原則式管理條件 | Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3f6f17e97b485e7c6c4dc747886bd5304b8fa812
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512363"
---
# <a name="create-a-new-policy-based-management-condition"></a>建立新的原則式管理條件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立原則式管理條件。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來建立條件：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-condition"></a>建立條件  
  
1.  在物件總管中，按一下加號，展開您想要建立原則式管理條件的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  按一下加號展開 **[Facet]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要建立新條件的 Facet，然後選取 [新增條件]。  
  
6.  在 **[建立新條件]** 對話方塊的 **[名稱]** 方塊中，輸入新條件的名稱。  
  
7.  在 **[Facet]** 清單中，確認正確的 Facet，或選取不同的 Facet。  
  
8.  在 **[運算式]** 底下的 **[欄位]** 方塊中選取 Facet 屬性及其相關聯的運算子和值，藉以建構條件運算式。 當您加入多個運算式時，可以使用 **[及]** 或 **[或]** 來聯結運算式。 如需此對話方塊可用之選項的詳細資訊，請參閱[建立新條件或開啟條件對話方塊，一般頁面](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)、[建立新條件或開啟條件對話方塊，描述頁面](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md)和[進階編輯 &#40;條件&#41; 對話方塊](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md)。  
  
9. 完成後，請按一下 **[確定]**。  
  
  
