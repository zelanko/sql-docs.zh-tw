---
title: 內嵌和共用資料連接或資料來源 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e507d9fa5b57fe63c1540f4490a7b04d878199f0
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288936"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>內嵌和共用資料連接或資料來源 (報表產生器及 SSRS)
  查詢執行或處理報表時，報表會使用資料連接擷取報表的資料。 您可以從內建的資料連接類型清單，選擇連接到關聯式資料庫、多維度資料庫、Web 服務或其他資料來源的類型。 下列項目可在描述資料連接時使用。  
  
-   **資料連接。** 也稱為 *資料來源*。 資料連接包括相依於連接類型的名稱和連接屬性。 依預設，資料連接不包括認證。 資料連接不會指定要從外部資料來源擷取的資料。 若要執行這項操作，您可以在建立資料集時指定查詢。  
  
-   **共用資料來源定義。** 包含報表資料來源之 XML 表示的檔案。 報表發行時，其資料來源會儲存到報表伺服器或 SharePoint 網站上做為資料來源定義，與報表定義分開。 例如，報表伺服器管理員可能會更新連接字串或認證。 在原生報表伺服器上，檔案類型為 .rds。 在 SharePoint 網站上，檔案類型為 .rsds。  
  
-   **連接字串。** 連接字串是連接到資料來源時所需之連接屬性的字串版本。 連接屬性會依資料連接類型而有所不同。 如需範例，請參閱＜ [報表產生器中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)＞。  
  
-   **共用資料來源。** 報表伺服器或 SharePoint 網站上提供的資料來源，可供多個報表使用。  
  
-   **內嵌資料來源。** 也稱為 *「報表特定資料來源」*(report-specific data source)。 在報表中定義而且僅供該報表使用的資料來源。  
  
-   **認證。** 認證是驗證資訊，您必須提供這項資訊才能存取外部資料。  
  
 內嵌與共用資料來源之間的差異在於建立、儲存和管理的方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>共用資料來源  
 如果資料來源使用頻率很高，則共用資料來源很有用。 建議您盡量使用共用資料來源。 它們會簡化報表和報表存取的管理，而且有助於提升報表和報表所存取之資料來源的安全性。 如果您需要共用資料來源，請要求系統管理員為您建立一個。  
  
 在報表產生器中，您無法建立共用資料來源。 您可以從報表伺服器瀏覽並選取共用資料來源。 如需詳細資訊，請參閱＜ [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)＞。  
  
 在報表設計師中，您無法瀏覽至報表伺服器上的共用資料來源。 您可以在 [方案總管] 中建立共用資料來源做為專案的一部分，並且選擇是否將它們部署到報表伺服器。 您可能因為電腦所需的認證和報表伺服器所需的認證不同，而選擇只在本機上使用這些共用資料來源。 如需詳細資訊，請參閱 [Reporting Services 中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 下列圖示表示報表伺服器資料夾階層中的共用資料來源項目：![共用資料來源圖示](media/hlp-16datasource.png "共用資料來源圖示")  
  
## <a name="embedded-data-sources"></a>內嵌資料來源  
 內嵌資料來源是儲存在報表定義中的資料連接。 內嵌資料來源連接資訊只能用於內嵌該資訊的報表中。 若要定義和管理內嵌資料來源，請使用 **[資料來源屬性]** 對話方塊。  
  
##  <a name="Comparing"></a> 比較內嵌與共用資料來源  
 下表摘要列出內嵌與共用資料來源之間的差異：  
  
|描述|內嵌<br /><br /> 資料來源|共用<br /><br /> 資料來源|  
|-----------------|------------------------------|----------------------------|  
|資料連接會內嵌在報表定義中。|![可用](media/greencheck.gif "可用")||  
|報表伺服器上資料連接的指標會內嵌在報表定義中。||![可用](media/greencheck.gif "可用")|  
|在報表伺服器上管理|![可用](media/greencheck.gif "可用")|![可用](media/greencheck.gif "可用")|  
|共用資料集所需||![可用](media/greencheck.gif "可用")|  
|元件所需||![可用](media/greencheck.gif "可用")|  
  
## <a name="data-source-credentials"></a>資料來源認證  
 認證用於建立內嵌資料來源、執行查詢，或是在處理報表時擷取資料。 資料來源連線的擁有者會決定您必須用於存取資料的認證類型。 認證會與報表伺服器、SharePoint 網站或報表撰寫環境中本機電腦上的資料連接分開管理。 根據資料來源的類型而定，認證可加以儲存並避免提示，或者設定為提示每一位使用者。 您需要的認證可能會依據您從電腦或是報表伺服器連接到資料來源而有所不同。 如需詳細資訊，請參閱 <<c0> [ 在報表產生器中指定認證](../../2014/reporting-services/specify-credentials-in-report-builder.md)並[資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [報表撰寫概念 &#40;報表產生器及 SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Reporting Services &#40;SSRS&#41; 支援的資料來源](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [內嵌和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
