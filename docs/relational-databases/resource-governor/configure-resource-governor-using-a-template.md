---
title: 使用範本設定資源管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 23b539444f2de609053d530df85edafcc58ba1f7
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582415"
---
# <a name="configure-resource-governor-using-a-template"></a>使用範本來設定資源管理員
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]所提供的範本來設定資源管理員。  
  
-   **開始之前：** [權限](#Permissions)  
  
-   **若要建立工作負載群組，請使用：**  [範本](#ConfRGTemplate)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 使用下列步驟即可開啟和修改建立資源集區與集區之工作負載群組的範本。 此外，這個範本可讓您建立使用者定義的分類函數，以便將新的連接路由傳送至預設群組或您所建立的工作負載群組。  
  
###  <a name="Permissions"></a> 權限  
 範本中的資源管理員 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式需要 CONTROL SERVER 權限。  
  
##  <a name="ConfRGTemplate"></a> 使用範本來設定資源管理員  
 **若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [檢視]  功能表上，按一下 [範本總管]  。  
  
2.  在 [範本總管]  中，展開 [Resource Governor]  ，然後按兩下 [設定 Resource Governor]  。  
  
3.  在 **[連接到 Database Engine]** 中，輸入必要資訊，然後按一下 **[確定]** 。 此時，[查詢編輯器] 就會提供 Configure Resource Governor.sql 範本。 您可以使用此範本來建立並設定資源集區、工作負載群組和分類函數。  
  
4.  若要變更範本中的值，請按下 CTRL+SHIFT+M。 在 **[指定範本參數的值]** 視窗中，輸入您想要使用的值。  
  
5.  若要儲存您對範本所做的變更，請按一下 **[確定]** 。  
  
6.  若要執行查詢，請按一下 **[執行]** 。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="see-also"></a>另請參閱  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [資源管理員工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [資源管理員分類函數](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [檢視資源管理員屬性](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
