---
title: 將自訂組件與報表搭配使用 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 94fdcbb6219aefb0cf38f0d77c0c3437ccf19915
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194092"
---
# <a name="using-custom-assemblies-with-reports"></a>將自訂組件與報表搭配使用
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，您可以為報表項目值、樣式和格式撰寫自訂程式碼。 例如，您可以使用自訂程式碼來根據地區設定格式化貨幣，以特殊格式設定某些值的旗標，或是為您的公司套用其他實施中的商務規則。 在報表中包括此程式碼的其中一個方法是，使用您可以從報表定義檔案中參考的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 來建立自訂程式碼組件。 伺服器會在報表執行時呼叫自訂組件中的函數。 自訂組件可用以擷取您計劃在報表中使用的特定函數。  
  
## <a name="in-this-section"></a>本節內容  
 [參考在 RDL 檔案中的組件](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
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
  
 [操作說明：對自訂組件進行偵錯](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 說明如何偵錯您的自訂組件程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [報表定義語言 &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
