---
title: 匯出封裝對話方塊 UI 參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- Export Package dialog box
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9e8943addabc92906bd0267d951fec5bda2113a5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376706"
---
# <a name="export-package-dialog-box-ui-reference"></a>匯出封裝對話方塊 UI 參考
  使用 **[匯出封裝]** 對話方塊 (可以從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中存取)，即可匯出 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝到不同的位置，並選擇性地修改封裝的保護等級。  
  
## <a name="options"></a>選項。  
 **封裝位置**  
 選取要用來儲存所匯出之封裝的儲存體類型。 下列是可以使用的選項：  
  
 **SQL Server**  
  
 **[File System]**  
  
 **SSIS 封裝儲存體**  
  
 **Server**  
 輸入伺服器名稱，或者從清單中選取一個伺服器。  
  
 **驗證**  
 選取 Windows 驗證或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證。 唯有儲存位置是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
> [!IMPORTANT]  
>  可能的話，請使用 Windows 驗證。  
  
 **驗證類型**  
 選取驗證類型。  
  
 **使用者名稱**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱。  
  
 **密碼**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供密碼。  
  
 **封裝路徑**  
 輸入封裝路徑，或按一下瀏覽按鈕 ([...])，並找出要儲存封裝的資料夾。  
  
 **保護等級**  
 按一下瀏覽按鈕 ([...]) 並更新 [封裝保護等級] 對話方塊中的保護等級。 如需詳細資訊，請參閱 [封裝與專案保護等級對話方塊](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)。  
  
## <a name="see-also"></a>另請參閱  
 [儲存封裝的副本](../../2014/integration-services/save-copy-of-package.md)   
 [匯入封裝對話方塊 UI 參考](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [儲存套件](save-packages.md)   
 [匯入和匯出封裝 &#40;SSIS 服務&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
