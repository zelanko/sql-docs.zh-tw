---
title: 文件和編寫 Analysis Services 資料庫的指令碼 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7862be07bd3b01db8dcc2a0beb115a883e4550e7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="document-and-script-an-analysis-services-database"></a>記錄和編寫 Analysis Services 資料庫的指令碼
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之後，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來輸出資料庫或資料庫所含之物件的中繼資料，作為 XML for Analysis (XMLA) 指令碼。 您可以將此指令碼輸出到新的 **[XMLA 查詢編輯器]** 視窗、到檔案或到剪貼簿。 如需 XMLA 的詳細資訊，請參閱 [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考 ](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
 產生的 XMLA 指令碼會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 元素，來定義指令碼所包含的物件。 如果您產生 CREATE 指令碼，則所產生的 XMLA 指令碼會包含 XMLA **Create** 命令和 ASSL 元素，您可用它們在執行個體上建立整個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫結構。 如果您產生 ALTER 指令碼，則所產生的 XMLA 指令碼會包含 XMLA **Alter** 命令和 ASSL 元素，您可用它們將現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫結構還原至建立指令碼時的資料庫狀態。  
  
 您有許多方式可以使用從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫產生的 XMLA 指令碼，包括：  
  
-   若要維護可讓您重新建立所有資料庫物件和權限的備份指令碼。  
  
-   若要建立或更新資料庫開發的程式碼。  
  
-   若要從現有的結構描述中建立測試或開發環境。  
  
## <a name="see-also"></a>另請參閱  
 [修改或刪除 Analysis Services 資料庫](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [建立項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
