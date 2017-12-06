---
title: "轉換 CRI 對話方塊 (報表產生器) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f532d0e554e85c7e302f3c8f9e61130179d51483
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="convert-cri-dialog-box-report-builder"></a>轉換 CRI 對話方塊 (報表產生器)
  此報表包含自訂報表項目 (CRI) 與不支援的功能。 CRI 是報表定義語言 (RDL) 的延伸模組，支援在報表中顯示資料的自訂物件。 CRI 包括軟體協力廠商所提供的設計階段和執行階段元件。  
  
> [!NOTE]  
>  選擇在報表伺服器上支援自訂報表項目是由系統管理員所做的決定。 若要檢視報表中的 CRI，必須在報表撰寫用戶端上安裝 CRI 元件才能預覽報表，並在報表伺服器上檢視已發行或已上傳的報表。  
  
 某些 CRI 可以轉換成新報表定義格式的報表項目。 當您開啟報表時，系統會提示您是否要升級。 您可以使用下列資訊來決定是否要轉換此報表中的 CRI：  
  
-   **是** ：選擇 **[是]** ，在可能的情況下轉換報表中的所有 CRI。 在 CRI 中不支援的功能無法升級，而且會從報表定義檔案中移除。 如需不支援的功能清單，請參閱 [升級報表](../../reporting-services/install-windows/upgrade-reports.md)。 檢視報表時，您可能會看到 CRI 在報表中顯示的方式有些差異。  
  
-   **否** ：當您不要轉換報表中的 CRI 時，選擇 **[否]** 。 這些 CRI 無法透過報表處理器顯示在其目前的版本中。 如果您的系統管理員打算安裝軟體協力廠商所提供，而且與新報表定義格式相容的新版 CRI，您應該選擇 **[否]**。 在新版本提供之前，CRI 會在報表中顯示為一個有紅色 X 的空文字方塊。  
  
 在任一種情況下，報表會升級到新的報表定義格式，並將原始報表的備份複本儲存為 *\<報表名稱>* `-` Backup.rdl。 如果您以報表撰寫工具儲存報表，您就是以新的報表定義格式儲存升級的報表。 如果您發行報表，此報表會先儲存在您的電腦中，然後再發行到報表伺服器。 您會將升級版本的報表發行至報表伺服器。  
  
 如果您沒有儲存報表，原始報表就會維持不變。 不過，您無法在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的更新版 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，或使用此報表定義格式的報表撰寫環境中編輯此報表。 您可以使用報表管理員將原始版本的報表上傳到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，繼續執行該報表。 如需詳細資訊，請參閱[上傳檔案或報表 &#40;報表管理員&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)。  
  
 對於您上傳 (而非發行) 到報表伺服器的報表，報表處理器會決定是否可以在第一次使用時升級報表。 無法升級的報表會在回溯相容性模式下處理，而且會如同在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中繼續顯示。 如需詳細資訊，請參閱 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)。  
  
 若要識別報表、報表伺服器或您報表撰寫環境的目前報表定義格式，請參閱[尋找報表定義結構描述版本 &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和精靈的報表產生器說明](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)  
  
  
