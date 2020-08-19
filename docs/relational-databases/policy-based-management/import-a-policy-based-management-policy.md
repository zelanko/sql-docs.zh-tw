---
description: 匯入原則式管理原則
title: 匯入原則式管理原則 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 37f49a006b0fe17120af2309f9b3991ab594ebda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423712"
---
# <a name="import-a-policy-based-management-policy"></a>匯入原則式管理原則
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中匯入原則式管理原則執行個體。  
  
## <a name="permissions"></a>權限
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。

  
##  <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
  
### <a name="to-import-a-policy-instance"></a>若要匯入原則執行個體  
  
1.  在物件總管**** 中，按一下加號，展開新匯入之原則執行個體所在的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  以滑鼠右鍵按一下 [原則]**** 資料夾，然後選取 [匯入原則]****。  
  
5.  在 [匯入]**** 對話方塊中，輸入檔案的路徑和名稱，或使用瀏覽 (**...**) 按鈕找出包含原則的 XML 檔案，然後選取此檔案。 如需有關 **[匯入]** 對話方塊可用之選項的詳細資訊，請參閱＜ [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md)＞。  
  
6.  完成後，請按一下 **[確定]** 。  


## <a name="example-policies"></a>範例原則
 範例原則不包含在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中，但先前的分散式範例原則可透過安裝 [SQL Server Management Studio v17](../../ssms/release-notes-ssms.md#previous-ssms-releases) 來存取。  安裝 SQL Server Management Studio v17 之後，就可以在 `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies` 中找到範例原則。 您可以匯入這些原則，並作為您自己的原則式管理原則使用。
