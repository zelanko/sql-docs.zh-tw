---
title: 從其他應用程式列印報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a5560581-fd57-4a45-b7ea-43b21a8a7419
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 67dc429871111c4e59f195b285c705622402c86b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33018745"
---
# <a name="print-reports-from-other-applications-report-builder-and-ssrs"></a>從其他應用程式列印報表 (報表產生器及 SSRS)
  報表產生器提供匯出選項，可以讓您輕鬆地在其他應用程式中檢視報表。 **Export** 命令提供於報表工具列上，當您在瀏覽器或網路架構應用程式中開啟報表時，此工具列會出現在報表頂端。 匯出報表會將報表顯示在不同的應用程式中 (例如，如果將報表匯出至 Excel，就會在 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]中開啟報表)。 若要列印，則建議只有當應用程式有您要使用的特定列印功能時，您才匯出報表。  
  
 若要將報表匯出至另一個應用程式，您必須已安裝該應用程式。 例如，在匯出為 Acrobat (PDF) 格式之前，您必須在電腦中安裝 Adobe Acrobat Reader。 如果選擇將報表匯出成 TIFF 格式，報表伺服器就會將報表放入與 TIFF 檔案類型關聯的檢視應用程式中。 雖然使用的應用程式會視您的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 版本而定，但通常此工具為 Windows 圖片和傳真檢視器。 預設的解析度對應於螢幕解析度 96 DPI。 您可以將 Windows 圖片和傳真檢視器的解析度增加至 300 DPI 或 600 DPI，以符合印表機的功能。 如需有關調整解析度的詳細資訊，請參閱 Windows 產品文件集。  
  
 如果您選擇網頁封存 (亦稱為 MHTML)，則報表將匯出至預設的瀏覽器。 從瀏覽器列印會造成在每一頁的底端加入報表路徑資訊。 在大部份的情況下，您可以設定瀏覽器選項，使其省略列印頁面上的路徑資訊。 如需詳細資訊，請參閱您使用之瀏覽器的產品文件集。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [使用列印控制項從瀏覽器列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [將報表匯出為其他檔案類型 &#40;報表產生器及 SSRS &#41;](http://msdn.microsoft.com/library/b577568b-ecbd-44c3-be88-31dab6fc38a2)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
