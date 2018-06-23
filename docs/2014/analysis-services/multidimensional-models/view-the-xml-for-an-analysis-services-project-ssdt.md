---
title: 檢視 Analysis Services 專案 (SSDT) 的 XML |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6af8a2dfc75889425aa8e86a9d44c65fe2da57df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147042"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>檢視 Analysis Services 專案的 XML (SSDT)
  當您在專案模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會針對專案資料夾中的每一個物件建立 XML 定義。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中檢視每一個物件之 XML 檔案的內容， 您也可以直接編輯 XML 檔案；但是，大多數情況下不建議您這樣做，因為您所做的變更可能會讓 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]無法讀取該 XML 檔案。  
  
> [!NOTE]  
>  您無法檢視整個專案的 xml 程式碼，但是可以檢視每一個物件的程式碼，因為每一個物件都有個別檔案存在。 唯一的方式檢視程式碼，以建置專案，並檢視 ASSL 是整個專案中的程式碼\<專案名稱 >.asdatabase 檔案。  
  
### <a name="to-view-the-xml-code-for-an-object"></a>檢視物件的 XML 程式碼  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 專案。  
  
2.  以滑鼠右鍵按一下方案總管中的物件，然後按一下 [檢視程式碼]。  
  
     此物件的 XML 程式碼即會出現在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中。  
  
## <a name="see-also"></a>另請參閱  
 [建立 Analysis Services 專案&#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
  