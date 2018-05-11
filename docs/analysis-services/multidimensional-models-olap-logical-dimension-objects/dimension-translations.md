---
title: 維度翻譯 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 091cdc3f770297e5fdf231582d5fd2d26d6e8c35
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dimension-translations"></a>維度翻譯
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  翻譯是一種簡單的機制，用來將顯示的標籤和標題從某個語言變成另一個語言。 每一個翻譯都會定義成一組值：具有翻譯文字的字串以及具有語言識別碼的數字。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的所有物件都可使用翻譯。 維度也可以將屬性值翻譯。 用戶端應用程式負責尋找使用者已定義的語言設定，並將所有標題和標籤切換成以該語言顯示。 物件可以有您想要的任何翻譯數目。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Translation> 物件是由語言識別碼和翻譯的標題所組成。 語言識別碼是**整數**語言 id。 翻譯的標題則是翻譯的文字。  
  
 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度翻譯就的維度，名稱名稱的特定語言表示法[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件或其中一個成員，例如標題、 成員或階層的層級。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也支援 cube 物件的翻譯。  
  
 翻譯會針對可支援多種語言的用戶端應用程式，提供伺服器支援。 通常，檢視 Cube 及其維度的使用者來自許多不同國家 (地區)。 可將 Cube 及其維度的各種元素翻譯成不同語言則十分有用，如此這些使用者就可檢視和了解 Cube。 例如，法國的商務使用者使用法文地區設定的工作站存取 Cube 時，就可用法文查看物件屬性值。 而德國的商務使用者使用德文地區設定的工作站存取相同 Cube 時，就可用德文查看相同的物件屬性值。  
  
 用戶端電腦的定序和語言資訊是以地區設定識別碼 (LCID) 的格式予以儲存。 連接時，用戶端將 LCID 傳遞至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 執行個體會使用 LCID 來決定在提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的中繼資料時要使用的翻譯集。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件不包含指定的翻譯，則使用預設語言來傳回內容給用戶端。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 翻譯](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Analysis Services 中的翻譯支援](../../analysis-services/translation-support-in-analysis-services.md)   
 [全球化秘訣和最佳作法 & #40;Analysis Services & #41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
