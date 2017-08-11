---
title: "報表中使用自訂組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0931134ffb0a1511a02a1919d0e68acc55d5f34b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="using-custom-assemblies-with-reports"></a>將自訂組件與報表搭配使用
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，您可以為報表項目值、樣式和格式撰寫自訂程式碼。 例如，您可以使用自訂程式碼來根據地區設定格式化貨幣，以特殊格式設定某些值的旗標，或是為您的公司套用其他實施中的商務規則。 在報表中包括此程式碼的其中一種方式是建立使用自訂程式碼組件[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]可以從報表定義檔案中參考。 伺服器會在報表執行時呼叫自訂組件中的函數。 自訂組件可用以擷取您計劃在報表中使用的特定函數。  
  
## <a name="in-this-section"></a>本節內容  
 [一種 RDL 檔案中的參考組件](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 描述如何參考報表定義語言檔案中的自訂組件。  
  
 [部署自訂組件](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 描述如何將自訂組件部署到報表設計師與報表伺服器。  
  
 [使用強式名稱自訂組件](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 描述如何使用自訂組件與強式名稱。  
  
 [自訂組件中的判斷提示權限](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 描述如何使用有限且特定的權限來部署自訂組件，以及如何判斷提示程式碼中的權限。  
  
 [透過運算式存取自訂組件](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 描述如何呼叫自訂組件方法做為報表定義中的報表運算式。  
  
 [初始化自訂組件物件](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 描述如何初始化從報表呼叫之自訂組件物件的值。  
  
 [如何： 偵錯自訂組件](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 說明如何偵錯您的自訂組件程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [報表定義語言 &#40;SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
