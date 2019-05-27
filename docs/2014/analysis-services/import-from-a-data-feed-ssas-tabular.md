---
title: 匯入從資料摘要 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb3a1cbcabc66492bbd780be4716ce69f15de37
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080564"
---
# <a name="import-from-a-data-feed-ssas-tabular"></a>從資料摘要匯入 (SSAS 表格式)
  資料摘要是從線上資料來源產生並串流至目的地文件或應用程式的一個或多個 XML 資料流。 您可以使用 [資料表匯入精靈]，將資料從資料摘要匯入模型。  
  
 本主題包含下列幾節：  
  
-   [了解從資料摘要匯入](#prereq)  
  
-   [從 Azure DataMarket 資料集匯入資料](#azure)  
  
-   [從公用或公司資料來源匯入資料摘要](#importdata)  
  
-   [從 SharePoint 清單匯入資料摘要](#importlist)  
  
-   [從 Reporting Services 報表匯入資料摘要](#importreport)  
  
##  <a name="prereq"></a> 了解從資料摘要匯入  
 您可以從下列類型的資料摘要，將資料匯入表格式模型：  
  
 **Reporting Services 報表**  
 您可以使用已經發行到 SharePoint 網站或報表伺服器的 Reporting Services 報表，做為模型中的資料來源。 從 Reporting Services 報表匯入資料時，您必須指定一個報表定義 (.rdl) 檔案做為資料來源。  
  
 **Azure DataMarket 資料集**  
 Azure DataMarket 是一種提供單一服務商場及資訊傳遞通道 (如雲端服務) 的服務。 Azure DataMarket 資料集需要的是帳號金鑰，而不是 Windows 使用者帳戶。  
  
 **Atom 摘要**  
 摘要必須是 Atom 摘要， 不支援 RSS 摘要。 摘要必須是可公開使用，或者您必須擁有權限可以使用目前登入的 Windows 帳戶連接到該摘要。  
  
 在匯入期間，資料摘要的資料只會加入模型一次。 若要從摘要取得已更新的資料，您可從模型設計師重新整理資料，或者在將模型部署到 Analysis Services 的實際執行個體之後，為模型設定資料重新整理排程。 如需詳細資訊，請參閱 [處理資料 &#40;SSAS 表格式&#41;](process-data-ssas-tabular.md)。  
  
##  <a name="azure"></a> 從 Azure DataMarket 資料集匯入資料  
 您可以從 Azure DataMarket 匯入資料做為模型中的資料表。  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>從 Azure DataMarket 資料集匯入資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[從資料來源匯入]**。 [資料表匯入精靈] 隨即開啟。  
  
2.  在 **[連接到資料來源]** 頁面上，選取 **[資料摘要]** 底下的 **[Azure DataMarket 資料集]**，然後按 **[下一步]**。  
  
3.  在 **[連接到 Azure DataMarket 資料集]** 頁面的 **[易記名稱]** 中，輸入所要存取之摘要的描述性名稱。 如果您要匯入多個摘要或資料來源，使用連接描述性名稱可有助於記住連接的使用方式。  
  
4.  在 **[資料摘要 URL]** 中，輸入資料摘要的位址。  
  
5.  在 **[安全性設定]** 的 **[帳號金鑰]** 中，輸入帳號金鑰。 Analysis Services 會使用帳號金鑰來存取 DataMarket 訂閱。  
  
6.  按一下 **[測試連接]** 確認可以使用摘要。 或者，您也可以按一下 **[進階]** ，以確認「基礎 URL」或「服務文件 URL」包含提供摘要的查詢或服務文件。  
  
7.  按 **[下一步]** 繼續執行匯入作業。  
  
8.  在 **[模擬資訊]** 頁面中，指定 Analysis Services 在重新整理資料時將用來連接資料來源的憑證，然後按 **[下一步]**。 這些憑證和帳號金鑰不同。  
  
9. 在精靈的 **[選取資料表和檢視表]** 頁面中，在 **[易記名稱]** 欄位輸入描述性名稱，讓該名稱指出匯入之後將包含此資料的資料表以便於識別。  
  
10. 按一下 **[預覽和篩選]** 來檢閱資料和變更資料行選取項目。 您不能限制匯入報表資料摘要中的資料列，但是可以藉由清除核取方塊移除資料行。 按一下 [確定] 。  
  
11. 在 **[選取資料表和檢視表]** 頁面中，按一下 **[完成]**。  
  
##  <a name="importdata"></a> 從公用或公司資料來源匯入資料摘要  
 您可以存取公用摘要，或建立自訂摘要服務，從專屬或舊版資料庫系統產生 Atom 摘要。  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>從公用或公司資料摘要匯入資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[從資料來源匯入]**。 [資料表匯入精靈] 隨即開啟。  
  
2.  在 **[連接到資料來源]** 頁面上，選取 **[資料摘要]** 底下的 **[其他摘要]**，然後按 **[下一步]**。  
  
3.  在 **[連接到資料摘要]** 頁面中，輸入所要存取之摘要的描述性名稱。 如果您要匯入多個摘要或資料來源，使用連接描述性名稱可有助於記住連接的使用方式。  
  
4.  在 **[資料摘要 URL]** 中，輸入資料摘要的位址。 有效值包括以下的值：  
  
    1.  包含 Atom 資料的 XML 文件。 例如，下列 URL 會指向 Open Government Data Initiative 網站上的公用摘要：  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  指定一個或多個摘要的 .atomsvc 文件。 .atomsvc 文件會指向提供一個或多個摘要的服務或應用程式。 每個摘要都指定為傳回結果集的基本查詢。  
  
         您可以指定位於 Web 伺服器上之 .atomsvc 文件的 URL 位址，也可以從電腦上的共用或本機資料夾開啟檔案。 如果在匯出 Reporting Services 報表時，曾經儲存一份 .atomsvc 文件至電腦中，您即會有一份該文件；或者，如果有人曾為您的 SharePoint 網站建立了資料摘要文件庫，那麼在該文件庫中就可能有多份 .atomsvc 文件。  
  
        > [!NOTE]  
        >  建議您指定可以透過 URL 位址或共用資料夾存取的 .atomsvc 文件，因為這樣可以讓您在將來，將活頁簿發行至 SharePoint 之後，為活頁簿設定自動資料重新整理。 如果您指定的不是位於您電腦上的本機位置，伺服器可以重複使用相同的 URL 位址或網路資料夾以重新整理資料。  
  
5.  按一下 **[測試連接]** 確認可以使用摘要。 或者，您也可以按一下 **[進階]** ，以確認「基礎 URL」或「服務文件 URL」包含提供摘要的查詢或服務文件。  
  
6.  按 **[下一步]** 繼續執行匯入作業。  
  
7.  在 **[模擬資訊]** 頁面中，指定 Analysis Services 在重新整理資料時將用來連接資料來源的憑證，然後按 **[下一步]**。  
  
8.  在精靈的 **[選取資料表和檢視表]** 頁面中，以描述性名稱取代 **[易記名稱]** 欄位中的「資料摘要內容」，讓該名稱指出匯入之後將包含此資料的資料表以便於識別。  
  
9. 按一下 **[預覽和篩選]** 來檢閱資料和變更資料行選取項目。 您不能限制匯入報表資料摘要中的資料列，但是可以藉由清除核取方塊移除資料行。 按一下 [確定] 。  
  
10. 在 **[選取資料表和檢視表]** 頁面中，按一下 **[完成]**。  
  
##  <a name="importlist"></a> 從 SharePoint 清單匯入資料摘要  
 您可以匯入 (SharePoint) 功能區上有 [匯出為資料摘要] 按鈕的任何 SharePoint 清單。 您可以按一下此按鈕，將清單匯出為摘要。  
  
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>從 SharePoint 清單匯入資料摘要  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[從資料來源匯入]**。  
  
2.  在 **[連接到資料來源]** 頁面上，選取 **[資料摘要]** 底下的 **[其他資料摘要]**，然後按 **[下一步]**。  
  
3.  在 **[連接到資料摘要]** 頁面中，輸入所要存取之摘要的描述性名稱。 如果您要匯入多個摘要或資料來源，使用連接描述性名稱可能有助於記住連接的使用方式。  
  
4.  在資料摘要 URL 輸入至清單資料服務的位址取代\<伺服器名稱 > 的 SharePoint 伺服器的實際名稱：  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  按一下 **[測試連接]** 確認可以使用摘要。 或者，您也可以按一下 **[進階]** ，以確認「服務文件 URL」包含清單資料服務的位址。  
  
6.  按 **[下一步]** 繼續執行匯入作業。  
  
7.  在 **[模擬資訊]** 頁面中，指定 Analysis Services 在重新整理資料時將用來連接資料來源的憑證，然後按 **[下一步]**。  
  
8.  在精靈的 **[選取資料表和檢視表]** 頁面中，選取您要匯入的清單。  
  
    > [!NOTE]  
    >  您只能匯入包含資料行的清單。  
  
9. 按一下 **[預覽和篩選]** 來檢閱資料和變更資料行選取項目。 您不能限制匯入報表資料摘要中的資料列，但是可以藉由清除核取方塊移除資料行。 按一下 [確定] 。  
  
10. 在 **[選取資料表和檢視表]** 頁面中，按一下 **[完成]**。  
  
##  <a name="importreport"></a> 從 Reporting Services 報表匯入資料摘要  
 如果您具備 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Reporting Services 部署，則可以使用 Atom 轉譯延伸模組，從現有的報表中產生資料摘要。  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>從已發行的 Reporting Services 報表匯入報表資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[從資料來源匯入]**。  
  
2.  在 **[連接到資料來源]** 頁面上，選取 **[資料摘要]** 底下的 **[報表]**，然後按 **[下一步]**。  
  
3.  在 [連接到 Microsoft SQL Server Reporting Services 報表] 頁面的 [易記連接名稱] 中，輸入所要存取之摘要的描述性名稱。 如果您要匯入多個資料來源，使用連接的描述性名稱可能有助於記住連接的使用方式。  
  
4.  按一下 **[瀏覽]** 以選取報表伺服器。  
  
     如果您定期使用報表伺服器上的報表，該伺服器可能會列在 **[最近使用的網站和伺服器]** 中。 否則，在 [名稱] 中輸入報表伺服器的位址，然後按一下 **[開啟]** 來瀏覽報表伺服器網站上的資料夾。 報表伺服器的範例位址可能是 http://\<電腦名稱 > / reportserver。  
  
5.  選取報表，並按一下 **[開啟]**。 或者，您可以在 **[名稱]** 文字方塊中貼上報表的連結，包括完整的路徑和報表名稱。 「資料表匯入精靈」會連接到報表，並在預覽區域中呈現出來。  
  
     如果報表有使用參數，您就必須指定參數，否則就無法建立報表連接。 這樣做的時候，只有與參數值相關的資料列才會匯入到資料摘要中。  
  
    1.  使用清單方塊，或是在報表中提供的下拉式方塊來選擇參數。  
  
    2.  按一下 **[檢視報表]** 更新資料。  
  
        > [!NOTE]  
        >  檢視報表將您所選取的參數和資料摘要定義儲存在一起。  
  
     選擇性地按一下 [進階]，為報表設定提供者專屬的屬性。  
  
6.  按一下 **[測試連接]** 確認可以將報表當做資料摘要使用。 或者，您也可以按一下 **[進階]** 來確認 **[內嵌服務文件]** 屬性包含指定資料摘要連接的內嵌 XML。  
  
7.  按 **[下一步]** 繼續執行匯入作業。  
  
8.  在 **[模擬資訊]** 頁面中，指定 Analysis Services 在重新整理資料時將用來連接資料來源的憑證，然後按 **[下一步]**。  
  
9. 在精靈的 **[選取資料表和檢視表]** 頁面中，選取要匯入做為資料之報表組件旁邊的核取方塊。  
  
     一些報表可能包含多個部分，包括資料表、清單或圖表。  
  
10. 在 **[易記名稱]** 方塊中，輸入您要在模型中儲存之資料摘要所在的資料表名稱。  
  
     如果沒有指派名稱，便會依預設使用 Reporting Service 控制項的名稱，例如 Tablix1、Tablix2。 建議您在匯入期間變更此名稱，這樣便能更輕易地識別匯入之資料摘要的來源。  
  
11. 按一下 **[預覽和篩選]** 來檢閱資料和變更資料行選取項目。 您不能限制匯入報表資料摘要中的資料列，但是可以藉由清除核取方塊移除資料行。 按一下 [確定] 。  
  
12. 在 **[選取資料表和檢視表]** 頁面中，按一下 **[完成]**。  
  
## <a name="see-also"></a>另請參閱  
 [支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [支援的資料類型 &#40;SSAS 表格式&#41;](tabular-models/data-types-supported-ssas-tabular.md)   
 [模擬 &#40;SSAS 表格式&#41;](tabular-models/impersonation-ssas-tabular.md)   
 [處理資料 &#40;SSAS 表格式&#41;](process-data-ssas-tabular.md)   
 [匯入資料 &#40;SSAS 表格式&#41;](import-data-ssas-tabular.md)  
  
  
