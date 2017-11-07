---
title: "文件和編寫 Analysis Services 資料庫的指令碼 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be00d2f69b130ff3787167062e97926ae141a869
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="document-and-script-an-analysis-services-database"></a>記錄和編寫 Analysis Services 資料庫的指令碼
  部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之後，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來輸出資料庫或資料庫所含之物件的中繼資料，作為 XML for Analysis (XMLA) 指令碼。 您可以將此指令碼輸出到新的 **[XMLA 查詢編輯器]** 視窗、到檔案或到剪貼簿。 如需 XMLA 的詳細資訊，請參閱 [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考 ](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
 產生的 XMLA 指令碼會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 元素，來定義指令碼所包含的物件。 如果您產生 CREATE 指令碼，則所產生的 XMLA 指令碼會包含 XMLA **Create** 命令和 ASSL 元素，您可用它們在執行個體上建立整個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫結構。 如果您產生 ALTER 指令碼，則所產生的 XMLA 指令碼會包含 XMLA **Alter** 命令和 ASSL 元素，您可用它們將現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫結構還原至建立指令碼時的資料庫狀態。  
  
 您有許多方式可以使用從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫產生的 XMLA 指令碼，包括：  
  
-   若要維護可讓您重新建立所有資料庫物件和權限的備份指令碼。  
  
-   若要建立或更新資料庫開發的程式碼。  
  
-   若要從現有的結構描述中建立測試或開發環境。  
  
## <a name="see-also"></a>請參閱＜  
 [修改或刪除 Analysis Services 資料庫](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [建立元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  

