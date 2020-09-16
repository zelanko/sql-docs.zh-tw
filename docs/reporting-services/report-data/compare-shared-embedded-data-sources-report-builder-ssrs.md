---
description: 比較共用和內嵌資料來源 - 報表產生器 & Reporting Services (SSRS)
title: 比較共用和內嵌資料來源 - 報表產生器與 Reporting Services | Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25721242123d34c1cb4b826cd937df2decf02523
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484991"
---
# <a name="compare-shared-and-embedded-data-sources---report-builder--reporting-services-ssrs"></a>比較共用和內嵌資料來源 - 報表產生器 & Reporting Services (SSRS)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]
 
您可以使用共用或內嵌的資料來源以連線到資料。 「共用資料來源」** 是獨立於所有報表外定義的。 您可以在報表伺服器或 SharePoint 網站的多份報表中使用共用資料來源。 「內嵌資料來源」** 則是在報表中定義。 您只能在該報表中使用內嵌資料來源。 

 如果資料來源使用頻率很高，則共用資料來源很有用。 建議您盡量建立並使用共用資料來源。 它們會簡化報表和報表存取的管理，而且有助於提升報表和報表所存取之資料來源的安全性。 如果需要共用資料來源，您可能必須要求系統管理員為您建立一個。  
  
 內嵌資料來源也稱為「報表特定資料來源」**，是儲存在報表定義中的資料連線。 內嵌資料來源連線資訊僅供資料來源內嵌所在的報表使用。 若要定義和管理內嵌資料來源，請使用 **[資料來源屬性]** 對話方塊。  
  
 內嵌與共用資料來源之間的差異在於其建立、儲存和管理的方式。  
  
-   在報表設計師中，您可以將內嵌或共用資料來源建立成 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 專案的一部分。 您可以控制要在本機使用它們進行預覽，還是將它們當做專案的一部分部署至報表伺服器或 SharePoint 網站。 您可以使用已經安裝在電腦以及報表伺服器或 SharePoint 網站 (部署報表的所在位置) 上的自訂資料延伸模組。  
  
     系統管理員可以安裝與設定其他資料處理延伸模組以及 .NET Framework 資料提供者。 如需詳細資訊，請參閱[資料處理延伸模組與 .NET Framework Data Providers &#40;SSRS&#41;](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)。  
  
     開發人員可以使用 <xref:Microsoft.ReportingServices.DataProcessing> API 建立資料處理延伸模組，以支援其他類型的資料來源。  
  
-   在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]中，您可以瀏覽至報表伺服器或 SharePoint 網站，然後選取共用資料來源或在報表中建立內嵌資料來源。 您無法在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 中建立共用資料來源。 您無法在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 中使用自訂資料延伸模組。  

## <a name="summary-of-differences"></a>差異摘要
  
 下表摘要列出內嵌與共用資料來源之間的差異。  
  
|描述|內嵌<br /><br /> 資料來源|共用<br /><br /> 資料來源|  
|-----------------|------------------------------|----------------------------|  
|資料連接會內嵌在報表定義中。|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|報表伺服器上資料連接的指標會內嵌在報表定義中。||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  
|在報表伺服器上管理|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  
|共用資料集所需||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  
|元件所需||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  

## <a name="next-steps"></a>後續步驟

[建立及管理共用資料來源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[建立和修改內嵌資料來源](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[設定部署屬性](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[指定報表資料來源的認證及連線資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
