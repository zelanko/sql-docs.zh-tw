---
title: 設定編頁報表的資料來源屬性 - SSRS | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5e134c81fd697d4aa6fc7e5b620c1a71ff462b73
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573199"
---
# <a name="configure-data-source-properties-for-a-paginated-report"></a>設定編頁報表的資料來源屬性
  當您執行編頁報表時，報表伺服器會擷取屬性資訊來判斷如何連線至資料來源。 資料來源類型、連接字串和認證資訊都是在已發行報表的 [資料來源] 屬性頁面中指定的。 您可以設定這些屬性，讓資料來源連接資訊與建立報表時所指定的原始值不同。  
  
 或者，如果您擁有已經指定您想要使用之連接資訊的預先定義共用資料來源，就可以改為指定此共用資料來源。 若要使用共用資料來源，請在報表的 [資料來源] 屬性頁面上，按一下 **[共用資料來源]** 。  
  
## <a name="to-configure-an-embedded-data-source"></a>若要設定內嵌資料來源  
  
1.  在 Web 入口網站中，巡覽至您要為其設定報表特定資料來源的報表。  
  
3.  選取右上角的省略符號 ( **...** ) > [管理]  。  
  
4.  按一下 [資料來源]  索引標籤。這會開啟報表的 [資料來源] 屬性頁面。  
  
5.  按一下 **[自訂資料來源]** ，即可在報表內部指定資料來源連接資訊。  
  
6.  在 **[連接類型]** 清單中，指定用來處理資料來源中之資料的資料處理延伸模組。  
  
7.  針對 **[連接字串]** ，請指定報表伺服器用於連接到資料來源的連接字串。 建議您不要在連接字串中指定認證。  
  
     下列範例將說明用以連線至本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的連接字串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  針對 **[使用下列方式連接]** ，指定報表執行時要如何取得認證：  
  
    -   如果您要提示使用者輸入登入名稱和密碼，請按一下 **[執行報表的使用者所提供的認證]** 。  
  
    -   如果您打算在具有支援訂閱或其他已排程之作業的報表 (例如自動化報表記錄產生) 中使用資料來源，請按一下 [安全地儲存在報表伺服器中的認證]  。  
  
    -   對於存取報表的使用者提供的認證，若要讓報表伺服器將認證傳送給主控外部資料來源的伺服器，請按一下 **[Windows 整合式安全性]** 。 在此情況下，不會提示使用者輸入使用者名稱或密碼。  
  
    -   如果資料來源沒有使用認證 (例如，如果資料來源是從檔案系統存取的 XML 檔)，請按一下 [不需要認證]  。 只有當這種認證類型適用於資料來源時，您才應該指定此認證類型。 如果您針對需要驗證的資料來源選取此選項，連接將會失敗。 如果您選取此選項，請務必設定自動執行帳戶，以便在使用者認證無法使用時，允許報表伺服器連接至其他電腦以擷取資料或檔案。  
  
 如需設定認證的詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。 如需自動執行帳戶的詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
## <a name="see-also"></a>另請參閱  
[建立、修改和刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[管理報表資料來源](../../reporting-services/report-data/manage-report-data-sources.md)
  
