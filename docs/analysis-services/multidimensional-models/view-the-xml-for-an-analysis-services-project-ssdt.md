---
title: 檢視 Analysis Services 專案 (SSDT) 的 XML |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1542c33d67c95c1c7154d08dbffd550b5f8cc72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>檢視 Analysis Services 專案的 XML (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您在專案模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會針對專案資料夾中的每一個物件建立 XML 定義。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中檢視每一個物件之 XML 檔案的內容， 您也可以直接編輯 XML 檔案；但是，大多數情況下不建議您這樣做，因為您所做的變更可能會讓 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]無法讀取該 XML 檔案。  
  
> [!NOTE]  
>  您無法檢視整個專案的 xml 程式碼，但是可以檢視每一個物件的程式碼，因為每一個物件都有個別檔案存在。 唯一的方式檢視程式碼，以建置專案，並檢視 ASSL 是整個專案中的程式碼\<專案名稱 >.asdatabase 檔案。  
  
### <a name="to-view-the-xml-code-for-an-object"></a>檢視物件的 XML 程式碼  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 專案。  
  
2.  以滑鼠右鍵按一下方案總管中的物件，然後按一下 [檢視程式碼]。  
  
     此物件的 XML 程式碼即會出現在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中。  
  
## <a name="see-also"></a>另請參閱  
 [建立 Analysis Services 專案 & #40;SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  
