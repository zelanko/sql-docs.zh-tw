---
title: "匯入封裝對話方塊 UI 參考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.importpackage.f1"
helpviewer_keywords: 
  - "匯入封裝對話方塊"
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 匯入封裝對話方塊 UI 參考
  使用 **[匯入封裝]** 對話方塊 (可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]存取)，即可匯入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，並設定或修改封裝的保護等級。  
  
## 選項。  
 **封裝位置**  
 選取要匯入封裝之儲存位置的類型。 下列是可以使用的選項：  
  
 **SQL Server**  
  
 **檔案系統**  
  
 **SSIS 封裝存放區**  
  
 **Server**  
 輸入伺服器名稱，或者從清單中選取一個伺服器。  
  
 **驗證**  
 選取 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 唯有儲存位置是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
> [!IMPORTANT]  
>  可能的話，請使用 Windows 驗證。  
  
 **驗證類型**  
 選取驗證類型。  
  
 **使用者名稱**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱。  
  
 **密碼**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供密碼。  
  
 **封裝路徑**  
 輸入封裝路徑，或按一下瀏覽按鈕 **(...)**，然後找出封裝。  
  
 **封裝名稱**  
 選擇性地重新命名封裝。 預設名稱是要匯入的封裝名稱。  
  
 **保護等級**  
 按一下瀏覽按鈕 **(...)** 並更新 **[封裝保護等級]** 對話方塊中的保護等級。 如需詳細資訊，請參閱[封裝與專案保護等級對話方塊](../../integration-services/packages/package-and-project-protection-level-dialog-box.md)。  
  
## 請參閱＜  
 [儲存封裝的副本](../Topic/Save%20Copy%20of%20Package.md)   
 [匯出封裝對話方塊 UI 參考](../../integration-services/service/export-package-dialog-box-ui-reference.md)   
 [儲存封裝](../../integration-services/save-packages.md)   
 [匯入和匯出封裝 &#40;SSIS 服務&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  