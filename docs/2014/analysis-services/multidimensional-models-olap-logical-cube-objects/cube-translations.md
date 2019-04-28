---
title: Cube 翻譯 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- cubes [Analysis Services], translations
- OLAP objects [Analysis Services], translations
- translations [Analysis Services], cubes
ms.assetid: 4e4fd6a4-d324-4508-b75a-2a57de9ab8ff
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c34024f61f5c7b42030e0acb848783e1acae3d6e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728496"
---
# <a name="cube-translations"></a>Cube 翻譯
  翻譯是一種簡單的機制，用來將顯示的標籤和標題從某個語言變成另一個語言。 每一個翻譯都會定義成一組值：具有翻譯文字的字串以及具有語言識別碼的數字。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的所有物件都可使用翻譯。 維度也可以將屬性值翻譯。 用戶端應用程式負責尋找使用者已定義的語言設定，並將所有標題和標籤切換成以該語言顯示。 物件可以有您想要的任何翻譯數目。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Translation> 物件是由語言識別碼和翻譯的標題所組成。 語言識別碼是具有語言識別碼的 `Integer`。 翻譯的標題則是翻譯的文字。  
  
 在  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，cube 翻譯是 cube 物件，例如，標題或顯示資料夾名稱的特定語言表示法。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也支援維度和成員名稱的翻譯。  
  
 翻譯會針對可支援多種語言的用戶端應用程式，提供伺服器支援。 通常會有不同國家 (地區) 的使用者檢視 Cube 資料。 可將 Cube 的各種元素翻譯成不同語言則十分有用，如此這些使用者就可檢視和了解 Cube 的中繼資料。 例如，法國的商務使用者使用法文地區設定的工作站存取 Cube 時，就可用法文檢視物件屬性值。 同樣地，德國的商務使用者使用德文地區設定的工作站存取相同 Cube 時，就可用德文檢視物件屬性值。  
  
 用戶端電腦的定序和語言資訊是以地區設定識別碼 (LCID) 的格式予以儲存。 連接時，用戶端將 LCID 傳遞至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 執行個體會使用 LCID 來決定要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的中繼資料提供給每個商務使用者時要使用的翻譯集。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件不包含指定的翻譯，則使用預設語言來傳回內容給用戶端。  
  
## <a name="see-also"></a>另請參閱  
 [維度翻譯](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [翻譯&#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [全球化秘訣和最佳做法 &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
