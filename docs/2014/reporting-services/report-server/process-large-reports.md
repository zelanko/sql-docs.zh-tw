---
title: 處理大型報表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], large reports
- page breaks [Reporting Services]
- large reports
- size [SQL Server], reports
- distributing reports [Reporting Services], large reports
ms.assetid: c5275a9f-c95b-46d7-bc62-633879a8a291
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4f86c02acfcefba4972769367649cfd6b2075107
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103614"
---
# <a name="process-large-reports"></a>處理大型報表
  大型報表會造成一定的處理挑戰，若要正確執行，就需要特定的組態。 除非將大型報表設定成支援分頁，否則不應視需要執行大型報表。  
  
> [!NOTE]  
>  依預設，會啟用分頁符號。 如果您認為報表會包含大量的資料，請勿停用分頁符號。 用於初始轉譯報表的 HTML 轉譯格式會在瀏覽器中開啟報表。 如果報表未分頁，所有的資料都會包含在單一頁面中，這是大多數瀏覽器都無法容納的。 例如，含有 5,000 個資料列資料的報表，很難在瀏覽器的單一頁面中檢視。  
  
 如果您是使用大型報表，應該選擇能夠容納大型文件的報表執行、轉譯，以及傳遞選項。 報表大小主要是從查詢傳回之資料列集，以及用於顯示報表的轉譯延伸模組所決定。  
  
 針對包含動態資料的報表，每次執行報表之後，報表大小有可能會大幅變更。 在此情況下，您應監視資料來源以判斷資料的變動性對您的報表有何影響，以及您是否必須遵循本主題中所指定的步驟。  
  
 如需如何診斷逾時錯誤和記憶體不足錯誤的詳細資訊和提示，請參閱 blogs.msdn.com 上的 [如何在報表伺服器中執行報表時診斷錯誤](https://go.microsoft.com/fwlink/?LinkId=85634) 文章。  
  
## <a name="configuration-recommendations"></a>組態建議  
 報表執行、報表轉譯與報表存取的建議包括下列項目：  
  
-   設計報表以支援分頁。 報表伺服器每次傳送一頁報表。 如果報表包含分頁，您就可以控制多少資料流至瀏覽器。 如需詳細資訊，請參閱 [預先載入快取 &#40;報表管理員&#41;](preload-the-cache-report-manager.md)。  
  
-   設定報表當成已排程的報表快照集執行，以防止其視需要執行。 請勿設定報表執行的逾時值。 在離峰時段執行報表。  
  
-   如果您要控制報表是否處理，請設定報表使用共用資料來源。 使用共用資料來源的一個優點，是您可以停用資料來源。 停用資料來源可避免處理報表。  
  
-   如果您想要節省磁碟空間，請停用報表記錄。 若要停用報表記錄，請清除 [記錄] 屬性頁面上所有的核取方塊。  
  
-   限制對報表的存取。 設定報表使用項目層級安全性，並以只允許需要的使用者存取之新角色指派取代預設的角色指派。  
  
     依預設，使用者可以開啟他們可在資料夾階層中檢視的任何報表。 即使設定報表以快照集執行，可在資料夾中檢視報表項目的使用者也可以開啟報表。 如果報表很大，則使用者在報表管理員中開啟報表時，可能會造成瀏覽器停止回應。  
  
## <a name="rendering-recommendations"></a>轉譯建議  
 在設定報表散發之前，重要的是了解哪些轉譯用戶端可容納大型文件。 建議的格式是使用軟分頁符號的預設 HTML 轉譯延伸模組，但是您可以選擇支援分頁的任何格式。  
  
 每一個轉譯格式的效能和記憶體耗用量各不相同。 相同的報表會視您選取的格式，而有不同的轉譯速度，且需要不同的記憶體數量。 最快速且記憶體需求較少的格式包括 CSV、XML 和 HTML。 PDF 和 Excel 的效能最慢，但其原因不同。 PDF 是屬於 CPU 運算密集的格式，Excel 則是 RAM 需求高的格式。 影像轉譯則介於這兩個群組之間。 您可以在定義如何散發報表時指定此格式。  
  
## <a name="deployment-and-distribution-recommendations"></a>部署與散發建議  
 如果您使用分頁符號來控制報表轉譯，則可以使用和部署任何報表一樣的方式來部署大型報表。 您可以透過報表管理員、SharePoint Web 組件或加入入口網站或網站的 URL，來提供報表的存取。 這些部署選項全都支援視需要存取，以及先前執行的報表快照集。  
  
 有一個替代部署策略，是將報表散發給個別使用者。 如果您能夠仔細設定傳遞選項的方式，就可以透過訂閱來散發大型報表。 您可以使用標準訂閱或資料驅動訂閱來傳遞報表。 訂閱和傳遞的建議包含下列各項：  
  
-   設定使用網頁封存 (MHTML)、PDF 或 Excel 的訂閱。  
  
-   如果您使用的是 PDF 或 Excel，請設定使用檔案共用傳遞的訂閱。 傳遞了報表之後，您可以使用桌面應用程式來處理報表。 您必須設定檔案共用的權限，以決定誰可以檢視報表。  
  
     請注意，一旦報表在檔案共用中，就不再受 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的控制或保護。 如果您要在更新報表時接獲通知，請建立使用電子郵件傳遞僅傳送通知的第二個訂閱。  
  
 如果您要使用電子郵件報表傳遞，請設定包含連結的訂閱。 避免將報表當成附加檔案傳送。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [設定報表處理屬性](set-report-processing-properties.md)   
 [指定報表資料來源的認證及連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](report-server-content-management-ssrs-native-mode.md)   
 [預先載入快取 &#40;報表管理員&#41;](preload-the-cache-report-manager.md)  
  
  
