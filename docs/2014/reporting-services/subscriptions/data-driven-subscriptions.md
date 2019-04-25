---
title: 資料驅動訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 964549d535fec50c0ec6e8dc17dd0ef2a1dda221
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62510919"
---
# <a name="data-driven-subscriptions"></a>資料驅動訂閱
  資料驅動訂閱會提供一個方式來使用在執行階段擷取自外部資料來源的動態訂閱資料， 資料驅動訂閱也可以使用在定義訂閱時所指定的靜態文字和預設值； 您可以使用資料驅動訂閱來執行下列作業：  
  
-   將報表散發給變動的訂閱者清單。 例如，您可以使用資料驅動訂閱，將報表散發至每個月的訂閱者都不同的整個大型組織內，或者使用決定現有使用者集內群組成員資格的其他準則。  
  
-   使用執行階段所擷取的報表參數值來篩選報表輸出。  
  
-   讓每一個報表傳遞的報表輸出格式和傳遞選項有所差異。  
  
 資料驅動訂閱是由多個部分所組成； 當您建立資料驅動訂閱時，會定義此訂閱的固定層面，這些層面包含以下內容：  
  
-   定義此訂閱所針對的報表 (訂閱一定會與單一報表有關聯)。  
  
-   用來散發此報表的傳遞延伸模組。 您可以指定報表伺服器電子郵件傳遞、檔案共用傳遞、用來預先載入快取的 Null 傳遞提供者或是自訂傳遞延伸模組， 但是不能指定單一訂閱內的多個傳遞延伸模組。  
  
-   訂閱者資料來源。 當您定義訂閱時，必須指定包含訂閱者資料之資料來源的連接字串； 訂閱者資料來源不能在執行階段動態指定。  
  
-   當您定義訂閱時，必須指定選取訂閱者資料所使用的查詢。 您不能在執行階段變更此查詢。  
  
 在處理訂閱時，會取得資料驅動訂閱中所用的動態值。 您可以在訂閱中使用的變動資料範例包括訂閱者名稱、電子郵件地址、慣用的報表輸出格式，或是對報表參數有效的任何值。 若要在資料驅動訂閱中使用動態值，您會在查詢中所傳回的欄位以及特定傳遞選項和報表參數之間定義對應。 每當處理此訂閱時，會從訂閱者資料來源中擷取變動資料。  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>使用資料驅動訂閱的需求  
 並非所有版本中都可以使用資料驅動訂閱功能， 您在執行階段可用來擷取訂閱資料的資料來源種類也有一些限制； 下列清單提供有關這些需求的詳細資訊：  
  
-   如需支援資料驅動訂閱功能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本詳細資訊，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
-   如果是訂閱資料，請選擇可以提供結構描述資訊給報表伺服器的資料來源； 支援資料來源類型的範例包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料、Oracle、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝資料、ODBC 資料來源和 OLE DB 資料來源。 如需訂閱者資料來源需求的詳細資訊，請參閱 [使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
## <a name="working-with-data-driven-subscriptions"></a>使用資料驅動訂閱  
 下列主題提供有關資料驅動訂閱的詳細資訊。  
  
|主題|描述|  
|------------|-----------------|  
|[建立、修改和刪除資料驅動訂閱](data-driven-subscriptions.md)|說明如何建立、修改或刪除資料驅動訂閱。|  
|[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|提供有關在資料驅動訂閱所使用之資料來源的資訊。|  
|[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)|提供逐步指示，以了解如何建立資料驅動訂閱。|  
|[快取報表 &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)|描述如何使用 Null 傳遞提供者搭配資料驅動訂閱，以預先載入快取。|  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [建立資料驅動訂閱頁面 &#40;報表管理員&#41;](../create-data-driven-subscription-page-report-manager.md)   
 [預先載入快取 &#40;報表管理員&#41;](../report-server/preload-the-cache-report-manager.md)  
  
  
