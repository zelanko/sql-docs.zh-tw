---
title: 使用 ReportViewer 控制項整合 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a9dbcf9efdb4febaf6a6647e754d31380e575727
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56009550"
---
# <a name="integrating-reporting-services-using-the-reportviewer-controls"></a>使用 ReportViewer 控制項整合 Reporting Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] 提供兩個 ReportViewer 控制項將報表檢視功能納入應用程式整合。 一個版本是用於 Windows Form 應用程式，另一個版本則是用於 Web Form 應用程式。 每個控制項都提供類似的功能，但是每個功能都是針對其個別的環境所設計的。 兩個控制項都可以處理已經部署到報表伺服器 (遠端處理模式) 的報表，或是已經複製到尚未安裝 (本機處理模式) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之電腦上的報表。  
  
 ReportViewer 控制項並未內建支援動態適應具備不同螢幕解析度之不同裝置的功能。  
  
## <a name="remote-processing-mode"></a>遠端處理模式  
 遠端處理模式是檢視已經部署到報表伺服器之報表的建議使用方法。 遠端處理模式提供下列優點：  
  
-   遠端處理可提供執行報表最佳化的方案，因為報表伺服器會處理報表。  
  
-   因為報表伺服器會處理所有的程序，所以報表要求可在向外延展部署中由多部報表伺服器處理，或在單一向上延展案例中由具備多個處理器的伺服器處理。  
  
 此外，在遠端模式中執行的報表可以利用報表伺服器的完整功能，包括所有的轉譯與資料延伸模組。  
  
> [!NOTE]  
>  當 ReportViewer 控制項在遠端處理模式下執行時，其可用的延伸模組清單須視安裝在報表伺服器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本而定。  
  
## <a name="local-processing-mode"></a>本機處理模式  
 本機處理模式提供替代的方法，可在未安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的情況下檢視和轉譯報表。 與遠端處理不同的是，只有報表伺服器提供的功能子集可在控制項中使用。 在本機處理模式中，資料處理不是由控制項來進行，而是由主機應用程式所實作。 但是，報表處理是由控制項本身所處理。 在本機處理模式中，只能使用 PDF、Excel、Word 和 Image 轉譯延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [將 Reporting Services 整合到應用程式](../application-integration/integrating-reporting-services-into-applications.md)   
 [建立 SSRS 報表，使用 Visual Studio (Curated Answer)](https://go.microsoft.com/fwlink/?LinkId=321991)  
  
  
