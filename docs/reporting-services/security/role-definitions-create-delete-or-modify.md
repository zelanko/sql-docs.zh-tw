---
description: 建立、刪除或修改角色 (Management Studio)
title: 建立、刪除或修改角色 (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a238f4421c86edea0d03ab52c1b739520f646222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423232"
---
# <a name="role-definitions---create-delete-or-modify"></a>角色定義 - 建立、刪除或修改

Reporting Services 會提供可定義報表伺服器之存取層級的預先定義角色。 需要存取報表伺服器的每個使用者或群組都會獲指派一個可定義所允許工作的角色。 這些角色完全是針對報表伺服器所定義。 在整個報表伺服器的所有區域定義和使用角色的方式都必須一致。

若要建立、修改或刪除角色，您可以使用 [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]。 您只能刪除未使用中的角色。

 若要將使用者和群組指派給您所建立的角色，請使用 SSRS Web 入口網站。 如需詳細資訊，請參閱[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)。

> [!NOTE]  
>如果報表伺服器是針對 SharePoint 整合模式所設定，而且您已連接至與報表伺服器整合的 SharePoint 網站，就可以檢視並修改權限等級，以便控制報表伺服器內容和作業的存取權。

## <a name="to-create-a-role-definition"></a>若要建立角色定義

1. 在 [物件總管] 中，展開報表伺服器節點。

2. 展開安全性資料夾。

3. 如果您要建立項目層級的角色定義，請以滑鼠右鍵按一下 [角色] > [新增角色]。

    或者，如果您要建立系統層級的角色定義，請以滑鼠右鍵按一下 [系統角色] > [新增系統角色]。

4. 為角色輸入唯一的名稱。 名稱至少必須包含一個字元。 它也可以包括空格和特定符號，但不得包括下列字元 `[; : \ / @ & = + , $ / * < > | "]`。

5. 選擇性地輸入描述。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，此描述僅會出現在本頁面上。 透過入口網站檢視此項目的使用者，可以在該工具中看到此描述。

6. 選取此角色成員可以執行的工作。

7. 選取 [確定]  。

### <a name="to-delete-or-modify-a-role-definition"></a>若要刪除或修改角色定義  

1. 在 [物件總管] 中，展開報表伺服器節點。

2. 展開安全性資料夾。

3. 若要刪除或修改項目層級的角色定義，請展開 [角色] 資料夾，然後執行下列其中一個動作：

    1. 若要刪除角色定義，請以滑鼠右鍵按一下項目 > [刪除]****。 [刪除目錄項目]**** 對話方塊隨即顯示。 選取 [確定]**** 以刪除角色。
  
    2. 若要修改角色定義，請以滑鼠右鍵按一下項目 > [屬性]****。 就會顯示 **[使用者角色屬性]** 對話方塊的 [一般] 頁面。

         選取此角色成員可以執行的工作，然後選取 [確定]****。
  
4. 若要刪除或修改系統層級角色定義，請展開 [系統角色]**** 資料夾。 執行下列其中一個動作：

- 若要刪除系統角色定義，請以滑鼠右鍵按一下項目，然後選取 [刪除]****。 [刪除目錄項目]**** 對話方塊隨即顯示。 選取 [確定]**** 以刪除角色。

- 若要修改系統角色定義，請以滑鼠右鍵按一下項目，然後選取 [屬性]****。 就會顯示 **[系統角色屬性]** 對話方塊的 [一般] 頁面。 選取此角色成員可以執行的工作，然後選取 [確定]**** 來套用變更。

## <a name="see-also"></a>另請參閱

 [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [建立和管理角色指派](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [SQL Server Management Studio 中的 Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
