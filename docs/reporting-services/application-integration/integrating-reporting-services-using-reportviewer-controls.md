---
title: 使用報表檢視器控制項進行整合
description: Visual Studio 提供兩個報表檢視器控制項，可將報表檢視功能整合到應用程式。
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
helpviewer_keywords:
- Report Viewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ce8530e2f7afb998c14838efb91c93d0b1cae3c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796859"
---
# <a name="integrate-reporting-services-using-report-viewer-controls"></a>使用報表檢視器控制項整合 Reporting Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 提供兩個報表檢視器控制項，可將報表檢視功能整合到應用程式。 一個版本是用於 Windows Form 應用程式，另一個版本則是用於 Web Form 應用程式。 每個控制項都提供類似的功能，但是每個功能都是針對其個別的環境所設計的。 兩個控制項都可以處理已經部署到報表伺服器的報表 (遠端處理模式)，或是已經複製到尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之電腦上的報表 (本機處理模式)。  
  
 報表檢視器控制項並未內建支援動態適應具有不同螢幕解析度的不同裝置。  
  
## <a name="remote-processing-mode"></a>遠端處理模式  
 遠端處理模式是檢視已經部署到報表伺服器之報表的建議使用方法。 遠端處理模式提供下列優點：  
  
-   遠端處理可提供執行報表最佳化的方案，因為報表伺服器會處理報表。  
  
-   因為報表伺服器會處理所有的程序，所以報表要求可在向外延展部署中由多部報表伺服器處理，或在單一向上延展案例中由具備多個處理器的伺服器處理。  
  
 此外，在遠端模式中執行的報表可以利用報表伺服器的完整功能，包括所有的轉譯與資料延伸模組。  
  
> [!NOTE]  
>  以遠端處理模式執行報表檢視器控制項時，其可用延伸模組清單必須取決於報表伺服器上所安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。  
  
## <a name="local-processing-mode"></a>本機處理模式  
 本機處理模式提供替代的方法，可在未安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的情況下檢視和轉譯報表。 與遠端處理不同的是，只有報表伺服器提供的功能子集可在控制項中使用。 在本機處理模式中，資料處理不是由控制項來進行，而是由主機應用程式所實作。 但是，報表處理是由控制項本身所處理。 在本機處理模式中，只能使用 PDF、Excel、Word 和 Image 轉譯延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [使用 WebForms 報表檢視器控制項](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [使用 WinForms 報表檢視器控制項](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
