---
title: 將報表發行 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c37897df36297323d164e382b6af081f2985eaf1
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59942674"
---
# <a name="publish-reports"></a>發行報表
  您可以從[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]部署專案，將報表伺服器專案中的所有報表與共用資料來源發行至報表伺服器，或者發行單一報表。 在可以發行報表之前，您必須指定目標報表伺服器的 URL。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md)。  
  
 您可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 版的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 來開啟、修改、預覽、儲存，以及同時發行 [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] 和 [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] 報表。 如需詳細資訊，請參閱 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
### <a name="to-publish-all-reports-in-a-project"></a>若要發行專案中的所有報表  
  
-   在 [組建] 功能表上，按一下 [部署 \<報表專案名稱>]。 或者，在方案總管中，以滑鼠右鍵按一下報表專案，然後按一下 [部署]。 您可以在 [輸出] 視窗中，檢視發行程序的狀態。  
  
    > [!NOTE]  
    >  當您部署報表伺服器專案時，也會部署報表專案中的共用資料來源。  
  
### <a name="to-publish-a-single-report"></a>若要發行單一報表  
  
-   在 [方案總管] 中，以滑鼠右鍵按一下報表，然後按一下 **[部署]**。 您可以在 [輸出] 視窗中，檢視發行程序的狀態。  
  
    > [!NOTE]  
    >  當您發行報表時，也必須部署該報表所使用的共用資料來源。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料來源與報表](reports/publishing-data-sources-and-reports.md)   
 [預覽報表](reports/previewing-reports.md)   
 [將報表發行至報表伺服器](reports/publishing-reports-to-a-report-server.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
