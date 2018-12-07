---
title: 檢視 SQL Server 物件的原則式管理 Facet | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 162b0f18759253ac5c842a88eb0027926a4c458b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521206"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>檢視 SQL Server 物件的原則式管理 Facet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中檢視套用至特定 SQL Server 物件的所有原則式管理 Facet。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目來檢視物件中的所有 Facet：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>若要檢視物件中的所有 Facet  
  
1.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體、執行個體物件、資料庫或資料庫物件，然後按一下 [Facet]。  
  
2.  在 **[檢視 Facet -***object_name*] 對話方塊的 [Facet] 清單中，選取要檢視其屬性的 Facet。 如需有關此對話方塊可用之選項的詳細資訊，請參閱＜ [View Facets Dialog Box](../../relational-databases/policy-based-management/view-facets-dialog-box.md)＞。  
  
3.  完成後，請按一下 **[確定]**。  
  
  
