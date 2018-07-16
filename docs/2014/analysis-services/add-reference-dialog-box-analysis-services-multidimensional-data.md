---
title: 加入參考對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0593f8a598894bbe08fb4657c980b208d8f29a64
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244062"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>加入參考對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [加入參考] 對話方塊，即可將參考加入 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 組件或開發專案的另一個專案中。 您可以在方案總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的 [組件] 資料夾，然後從內容功能表中選取 [新增組件參考]，來顯示 [加入參考] 對話方塊。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**.NET**|選取此索引標籤即可將參考加入已註冊的元件中。 這個索引標籤會顯示方格，而這個方格包含已註冊之 .NET Framework 元件的清單。 從方格中選取一或多個項目，然後按一下 [加入] 將選取的 .NET 元件加入 [選取的產品和元件] 中。 此方格包含下列資料行：<br /><br /> **元件名稱**：元件的完整或「易記」名稱。 選取依元件名稱排序的標題。<br /><br /> **版本**： 元件的列出的版本號碼。 選取依版本排序的標題。<br /><br /> **執行階段**： 元件所依據的.NET framework 版本。 選取依執行階段版本排序的標題。<br /><br /> **路徑**： 元件以及其所在的路徑的檔案名稱。 選取依路徑排序的標題。|  
|**瀏覽**|按一下即可針對未在 [.NET] 或 [最近使用的] 索引標籤中列出的組件，瀏覽其檔案系統。 此索引標籤顯示下列選項：<br /><br /> **查看**： 從下拉式清單中選取的資料夾。 從此清單中選取資料夾會在主窗格中顯示該資料夾的內容。<br /><br /> **移至 瀏覽的最後一個資料夾**： 傳回**查看**至上一個位置。<br /><br /> **上一層**： 尋找階層中的下一個較高的資料夾。<br /><br /> **建立新資料夾**： 選取即可建立新的子資料夾中選取的資料夾之下**查看**。<br /><br /> **檢視功能表**： 若要變更在主窗格中的目錄檢視中選取。  如需 [檢視功能表] 中選項的詳細資訊，請參閱 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 文件集內的＜檢視檔案和資料夾概觀＞主題。 下列是可以使用的選項：<br />縮圖<br />並排顯示<br />圖示<br />清單<br />詳細資料<br /><br /> **主窗格**： 會顯示在選取的資料夾的內容**查看**。 選取一或多個項目，然後按一下**新增**新增至選取的檔案**選取的產品和元件**。 如需有關主窗格中之選項和內容功能表的詳細資訊，請參閱  Windows 文件集內的＜檢視檔案和資料夾概觀 (Viewing files and folders overview)＞主題。<br /><br /> **檔案名稱**： 使用此選項可篩選的檔案和資料夾，會顯示。 鍵入要篩選的完整或部份檔案名稱。 您可以使用星號 (\*) 作為萬用字元。 鍵入多個檔案名稱 (以雙引號 (") 括住每個檔案名稱並以空格分隔) 以選取多個檔案。 您也可以從下拉式清單中選取檔案名稱，來選取先前檢閱過的檔案。 提示： 您可以找出 Web 伺服器和網路電腦輸入中的 URL 或網路路徑**檔案名**。 例如，"http://mywebsite" 會顯示在 "mywebsite" Web 位置上的可用檔案，而 "\\\myserver\myshare" 則會顯示在 "myserver" 的 "myshare" 位置上的可用檔案。<br /><br /> **檔案類型**： 使用此選項可篩選的資料夾或目錄中選取的內容**查看**針對特定的檔案類型。|  
|**最近**|顯示最近加入 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案中的元件參考清單。 從方格中選取一或多個項目，然後按一下 [加入] 將選取的 .NET Framework 組件加入 [選取的產品和元件] 中。 方格包含下列資料行：<br /><br /> **元件名稱**：元件的完整或「易記」名稱。 選取依元件名稱排序的標題。<br /><br /> **版本**： 元件的列出的版本號碼。 選取依版本排序的標題。<br /><br /> **執行階段**： 元件所依據的.NET framework 版本。 選取依執行階段版本排序的標題。<br /><br /> **路徑**： 元件以及其所在的路徑的檔案名稱。 選取依路徑排序的標題。|  
|**[加入]**|按一下即可將 [.NET]、[瀏覽] 或 [最近使用的] 索引標籤中選取的元件加入 [選取的專案和元件] 中。|  
|**移除**|按一下即可移除在 [選取的專案和元件] 中選取的元件。|  
|**選取的專案和元件**|顯示要加入 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的元件參考清單。 從方格中選取一或多個項目，然後按一下 [移除] 將選取的元件從方格中移除。 方格包含下列資料行：<br /><br /> **元件名稱**：元件的完整或「易記」名稱。 選取依元件名稱排序的標題。<br /><br /> **版本**： 元件的列出的版本號碼。 選取依版本排序的標題。<br /><br /> **執行階段**： 元件所依據的.NET framework 版本。 選取依執行階段版本排序的標題。<br /><br /> **路徑**： 元件以及其所在的路徑的檔案名稱。 選取依路徑排序的標題。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型組件管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
