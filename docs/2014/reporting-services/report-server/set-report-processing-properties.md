---
title: 設定報表處理屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- on-demand reports
- report processing [Reporting Services], execution properties
- snapshots [Reporting Services], running reports from
- cached reports [Reporting Services]
- report snapshots [Reporting Services], running reports from
- report execution snapshots [Reporting Services]
ms.assetid: b5cbc453-5986-423e-af44-1f243ef3edb1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d03a03aeec28f6aef2f1c62ea62c0500be2bf435
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190856"
---
# <a name="set-report-processing-properties"></a>設定報表處理屬性
  報表執行屬性控制處理報表的方式。 您必須針對每個報表個別設定執行屬性。  
  
 若要設定報表執行屬性，請在報表管理員中開啟報表，然後導覽到 [執行] 屬性頁面。 您也可以設定屬性使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 如需詳細資訊，請參閱[處理選項屬性頁面 &#40;報表管理員&#41;](../processing-options-properties-page-report-manager.md)。  
  
## <a name="report-execution-modes"></a>報表執行模式  
 您可以視需要或以快照集的形式執行報表。 下一節描述每一種方法。  
  
### <a name="running-reports-on-demand"></a>視需要執行報表  
 您可以指定每次使用者執行報表時，報表便查詢資料來源，產生包含最新資料的視需要執行報表。 針對開啟或要求報表的每個使用者，會建立報表的一個新執行個體；每個新執行個體均包含一個新查詢的結果。 使用此方法時，如果十位使用者同時開啟報表，則會傳送十個查詢至資料來源進行處理。  
  
### <a name="running-reports-on-demand-from-cache"></a>從快取視需要執行報表  
 若要增強效能，您可以指定當使用者執行報表時，暫時快取報表 (與資料)。 快取副本後續可供其他存取相同報表的使用者使用。 使用此方法，如果有十個使用者開啟報表，則只有第一個要求會產生報表處理。 然後報表會快取，其餘九個使用者則檢視快取的報表。  
  
 快取報表會按照您定義的間隔，從快取移除。 間隔可以指定為分鐘，或者您可以安排特定的日期和時間來清空快取。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
### <a name="running-reports-from-snapshots"></a>從快照集執行報表  
 報表快照集是一種報表，它包含配置資訊以及在特定時間點擷取的資料。 您可以將報表以報表快照集的形式執行，以避免在任意時間 (例如，在排程備份期間) 執行報表。 報表快照集一般會按照排程建立和後續重新整理，讓您可以設定報表以及資料處理進行的正確時間。 如果報表所依據的，是要花很長時間執行的查詢，或者使用您希望在幾個小時內沒有人能存取之資料來源中之資料的查詢，您應將報表當成快照集執行。  
  
 報表快照集會儲存在報表伺服器資料庫中，後續若有使用者或處理序 (例如訂閱) 要求報表，就會從資料庫擷取報表快照集。 報表快照集更新時，會以新的執行個體覆寫。 除非您特別設定選項，將報表快照集的舊版本加入至報表記錄，否則報表伺服器不會儲存報表快照集的舊版本。 如需詳細資訊，請參閱 [建立、修改及刪除報表記錄中的快照集](create-modify-and-delete-snapshots-in-report-history.md)。  
  
 並非所有的報表都能設定以快照集執行。 您無法針對會提示使用者輸入認證的報表，或者使用 Windows 整合式安全性以取得報表資料的報表，建立報表的快照集。 如果您要將參數化報表當成快照集執行，則必須指定建立快照集時使用的預設參數。 相對於視需要執行的報表，一旦報表開啟之後，您就無法再為報表快照集指定不同的參數值。 選擇其他參數值會產生新的報表處理要求，這是不允許的。  
  
 在某些情況下，設定視需要報表當成快照集執行可能會停用訂閱。 下列情況會導致報表伺服器停用原先設定報表視需要執行時所定義之現有的訂閱：  
  
-   報表使用查詢參數，而您選取特定值當做預設參數，以滿足將報表當成快照集執行的需求。  
  
-   現有的訂閱設定成使用與您為快照集指定之預設參數值不同的參數值。  
  
 如果有這種情況，報表伺服器就會在下次訂閱排程執行時停用訂閱。 若要重新啟動訂閱，請開啟再儲存訂閱。 當您開啟訂閱，報表伺服器會將訂閱參數值更新為快照集所指定的值。 如需訂用帳戶的詳細資訊，請參閱[訂用帳戶與傳遞 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [設定報表的執行屬性 &#40;報表管理員&#41;](../reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Reporting Services 概念 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [如何：將快照集加入報表記錄](add-a-snapshot-to-report-history-report-manager.md)   
 [指定報表資料來源的認證及連線資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
