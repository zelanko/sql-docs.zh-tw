---
title: 將自訂組件與報表搭配使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e79f48f4e4a2eb5fbc83c353461709658caf2509
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63265660"
---
# <a name="using-custom-assemblies-with-reports"></a>將自訂組件與報表搭配使用
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，您可以為報表項目值、樣式和格式撰寫自訂程式碼。 例如，您可以使用自訂程式碼來根據地區設定格式化貨幣，以特殊格式設定某些值的旗標，或是為您的公司套用其他實施中的商務規則。 在您的報表中包含此程式碼的其中一個方法是，使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]您可以從報表定義檔案中參考的來建立自訂程式碼元件。 伺服器會在報表執行時呼叫自訂組件中的函數。 自訂組件可用以擷取您計劃在報表中使用的特定函數。  
  
## <a name="in-this-section"></a>本節內容  
 [參考在 RDL 檔案中的組件](referencing-assemblies-in-an-rdl-file.md)  
 描述如何參考報表定義語言檔案中的自訂組件。  
  
 [部署自訂組件](deploying-a-custom-assembly.md)  
 描述如何將自訂組件部署到報表設計師與報表伺服器。  
  
 [使用強式名稱自訂組件](using-strong-named-custom-assemblies.md)  
 描述如何使用自訂組件與強式名稱。  
  
 [自訂組件中的判斷提示權限](asserting-permissions-in-custom-assemblies.md)  
 描述如何使用有限且特定的權限來部署自訂組件，以及如何判斷提示程式碼中的權限。  
  
 [透過運算式存取自訂組件](accessing-custom-assemblies-through-expressions.md)  
 描述如何呼叫自訂組件方法做為報表定義中的報表運算式。  
  
 [初始化自訂組件物件](initializing-custom-assembly-objects.md)  
 描述如何初始化從報表呼叫之自訂組件物件的值。  
  
 [如何：針對自訂組件進行偵錯](how-to-debug-custom-assemblies.md)  
 說明如何偵錯您的自訂組件程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [報表定義語言 &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)  
  
  
