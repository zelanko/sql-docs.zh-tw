---
title: "報表設計師中的報表組件 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rtp.rptdesigner.components.f1
ms.assetid: 0c34311d-05d6-4bd2-b452-545fa95f8e7f
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 1060d0f256f9520860b01d4c324bd8e21100e923
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="report-parts-in-report-designer-ssrs"></a>報表設計師中的報表組件 (SSRS)

  在報表設計師中，建立專案的資料表、圖表及其他分頁報表項目之後，您可以將它們當作*「報表組件」*發行至報表伺服器或與報表伺服器整合的 SharePoint 網站，以供您和其他人員在其他報表中重複使用這些組件。  
  
 一般來說，報表組件在報表設計師和報表產生器中的運作方式都相同。 若要了解基本功能，請參閱[報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
 報表組件在報表設計師中運作的方式有基本的差異。 主要差異在於工作流程。 報表產生器可進行共同作業式撰寫：我建立報表組件並加以發行。 您可以重複使用、修改，並重新發行。 在報表設計師中，發行作業是單向的：我可以從報表設計師發行報表組件，而且您可以重複使用它。 但是，我無法在報表設計師的報表中重複使用現有的報表組件。 本主題會先快速介紹報表組件的概觀，然後再詳細說明這些差異。  
  
##  <a name="ComponentWorkflow"></a> 報表組件發行的生命週期  
 ![rs_ComponentCreation](../../reporting-services/report-design/media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  在報表設計師中，某甲建立專案，其中包含的報表具有以內嵌資料集為依據的圖表。  
  
2.  某甲為含內嵌資料集的圖表加上旗標，以供發行。 報表設計師為它指派唯一識別碼。 然後，某甲將報表部署至報表伺服器。 報表設計師發行該圖表。  
  
3.  某乙在報表產生器中建立空白報表，並將圖表加入其中。 現在，該圖表加上內嵌資料集都是某乙報表的一部分。 某乙可以修改報表中的圖表執行個體與資料集。 這項作業對報表伺服器上的圖表執行個體和資料集不會有任何影響，也不會中斷報表中與報表伺服器上執行個體之間的關聯性。  
  
     ![rs_BIDScomponentupdate](../../reporting-services/report-design/media/rs-bidscomponentupdate.gif "rs_BIDScomponentupdate")  
  
4.  在報表設計師中，某甲修改原始報表中的圖表。  
  
5.  某甲重新部署報表，將該圖表重新發行至伺服器，因而更新了伺服器上的圖表。  
  
6.  在報表產生器中，某乙接受來自伺服器的已更新圖表。 這會覆寫某乙在自己報表中對圖表所做的變更。  
  
##  <a name="PublishingComponents"></a> 發行報表組件  
 當您發行報表組件時，報表設計師會為它指派唯一的識別碼。 此後，它就維持該識別碼，無論您做什麼變都一樣。 識別碼會連結您報表中的原始報表項目至報表組件。 當其他報表作者在報表產生器中重複使用此報表組件時，該識別碼也將他們的報表連結到該報表組件。  
  
 以下是您可以發行為報表組件的報表項目：  
  
-   圖表  
  
-   量測計  
  
-   影像和內嵌影像  
  
-   地圖  
  
-   參數  
  
-   矩形  
  
-   資料表  
  
-   矩陣  
  
-   清單  
  
 如果您發行的報表組件會顯示資料，如資料表、矩陣或圖表，您可以共用資料集為其根據，否則，當您發行該報表組件時，所根據的資料集會儲存為內嵌資料集。 內嵌資料集可以使用內嵌資料集來源為根據，但認證並未儲存於內嵌資料集來源中。 因此，如果您的報表組件是以使用內嵌資料來源的內嵌資料集為依據，任何人只要重複使用此報表組件都必須提供內嵌資料來源的認證。 若要避免這種情形，請以含預存認證的共用資料來源做為內嵌和共用資料集的根據。 如需詳細資訊，請參閱 [報表產生器中的報表組件和資料集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)。  
  
 在報表設計師中發行報表組件的程序有兩個步驟：  
  
1.  在 **[發行報表組件]** 對話方塊中，將您要發行的報表項目加上旗標。  
  
2.  部署報表。  
  
 部署報表時，報表組件會發行至 SharePoint 網站或報表伺服器，讓其他人也可以重複使用。 若要發行報表組件，必須具有報表伺服器的連線，並在部署報表時具有該伺服器上足夠的權限。  
  
  
##  <a name="SearchReuseComponents"></a> 重複使用報表組件  
 跟報表產生器不同的是：您無法在建立報表組件之專案外的任何專案中，搜尋並重複使用該報表組件。  
  
 在報表產生器中工作的報表作者可以在他們建立的報表中，搜尋並重複使用您所發行的報表組件。  
  
##  <a name="RepublishingComponents"></a> 重新發行報表組件  
 在報表設計師中，您必須從建立組件的報表之中，更新現有的報表組件。 在報表產生器中，報表作者可以重複使用報表組件，並將其發行為新的報表組作，而不會取代您所發行的報表組件。 如果有足夠的權限，他們也可以更新您所發行的報表組件。 任何人只要在網站或伺服器上具有足夠的資料夾權限，都可以更新儲存於該處的報表組件。 最後的更新會覆寫先前的更新。  
  
 您可以修改，然後將報表組件重新發行到網站或伺服器。 報表產生器報表作者如果已經將該報表組件加入報表中，下次開啟該報表時就會接到變更的通知。 他們可以選擇接受您所做的變更與否。  
  
 您也可以選擇將已經發行過的報表當做新報表來發行。 請在 [發行報表組件] 對話方塊中，按一下 [發行為新報表組件]。 這個新的報表組件會有新的唯一識別碼，而且和舊的報表組件沒有關聯性。  

## <a name="next-steps"></a>後續的步驟

[管理報表組件](../../reporting-services/report-design/managing-report-parts.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
