---
title: 排程資料重新整理 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 8571208f-6aae-4058-83c6-9f916f5e2f9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58764334a6ee1902a09941e9fc9bb9723e517cdf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363840"
---
# <a name="schedule-a-data-refresh-powerpivot-for-sharepoint"></a>排程資料重新整理 (PowerPivot for SharePoint)
  您可以排程資料重新整理，以取得已發行到 SharePoint 網站之 Excel 活頁簿內對 PowerPivot 資料的自動更新。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 **本主題內容：**  
  
 [必要條件](#prereq)  
  
 [資料重新整理概觀](#intro)  
  
 [啟用和排程資料重新整理](#drenablesched)  
  
 [確認資料重新整理](#drverify)  
  
> [!NOTE]  
>  PowerPivot 資料重新整理是由在 SharePoint 伺服陣列中的 Analysis Services 伺服器執行個體所執行。 它與在 Excel Services 中提供的資料重新整理功能不相關。 PowePivot 排程資料重新整理功能不會重新整理非 PowerPivot 資料。  
  
##  <a name="prereq"></a> 必要條件  
 您必須在活頁簿上擁有「參與」權限層級或更高的權限層級，才能建立資料重新整理排程。  
  
 在資料重新整理期間所存取的外部資料來源必須是可用的，而且您在排程中指定的認證必須具有存取這些資料來源的權限。 排程資料重新整理需要可透過網路連線存取的資料來源位置 (例如，從網路檔案共用，而非您工作站上的本機資料夾)。  
  
 資料來源不得為 Office 文件或 Access 資料庫。 Office 不支援在伺服器環境中使用 Office 資料連接元件。 如果您的活頁簿中包含這些來源中的資料，請務必從資料重新整理排程中的資料來源清單移除這些來源。  
  
 活頁簿必須是 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本。 如果您使用在舊版 PowerPivot for Excel 中建立的活頁簿，除非您將資料庫升級到最新版本，否則排程資料重新整理無法運作。  
  
 在完成重新整理作業時必須簽入活頁簿。 活頁簿的鎖定是在資料重新整理結束時，在儲存檔案時對檔案施加鎖定，而不是在重新整理開始時。  
  
> [!NOTE]  
>  當資料重新整理正在進行中時，伺服器不會鎖定活頁簿。 不過，它會在資料重新整理結束時鎖定檔案，以簽入更新的檔案。 如果此時將檔案簽出到其他使用者，將會擲回重新整理的資料。同樣地，如果檔案已簽入，但它與伺服器在資料重新整理開始時所擷取的副本明顯不同，則會捨棄重新整理的資料。  
  
##  <a name="intro"></a> 資料重新整理概觀  
 Excel 活頁簿中的 PowerPivot 資料可能源自多個外部資料來源，包括您從遠端伺服器或網路檔案共用存取的外部資料庫或資料檔案。 對於包含從連接或外部資料來源匯入之資料的 PowerPivot 活頁簿，您可以設定資料重新整理，以便排程從這些原始來源自動匯入更新資料。  
  
 外部資料來源是透過您指定的內嵌連接字串、URL 或 UNC 路徑來存取，這些是您在使用 PowerPivot 用戶端應用程式，將原始資料匯入活頁簿時所指定。 儲存在 PowerPivot 活頁簿中的原始連接資訊會在後續的資料重新整理作業中重複使用。 您可以覆寫用來連接資料來源的認證，但是您無法覆寫用於資料重新整理的連接字串；僅能使用現有的連接資訊。  
  
 每個活頁簿中，只有一個資料重新整理排程頁面，在該頁面上指定所有排程資訊。 一般而言，撰寫活頁簿的人員會定義排程。  
  
 身為排程擁有者，您將會執行下列工作：  
  
-   定義預設排程。 這就是在資料來源層級上沒有定義排程時所用的排程。  
  
-   指定用來執行資料重新整理的認證。  
  
-   選擇要包含在重新整理作業中的資料來源。  
  
-   選擇性地為資料重新整理期間查詢的每個資料來源，指定內嵌、個別的排程及認證。 每個資料來源可獨立重新整理。 如果您為每個資料來源建立自訂排程，就會忽略預設排程。  
  
 為個別的資料來源建立細微的排程，可讓您使重新整理排程符合外部資料來源的波動。 例如，如果外部資料來源包含在一天內產生的交易資料，則可以為該資料來源建立個別的資料重新整理排程，以取得它每晚的更新資訊。  
  
##  <a name="drenablesched"></a> 啟用和排程資料重新整理  
 請使用下列指示，來為已發行到 SharePoint 文件庫之 Excel 活頁簿中的 PowerPivot 資料，排程資料重新整理。  
  
1.  在包含活頁簿的文件庫中選取活頁簿，然後按一下向下箭號以顯示命令清單。  
  
2.  按一下 **[管理 PowerPivot 資料重新整理]**。 如果已經定義資料重新整理排程，則會改看到 [檢視資料重新整理] 記錄頁面。 您可以按一下 **[設定資料重新整理]** 以開啟排程定義頁面。  
  
3.  在排程定義頁面中，選取 **[啟用]** 核取方塊。  
  
4.  在 [排程詳細資料] 中，指定排程的類型並指定其詳細資料。 此步驟建立預設排程。  
  
    > [!IMPORTANT]  
    >  請務必選取 **[並且盡快重新整理]** 核取方塊。 此選項可讓您驗證此活頁簿的資料重新整理功能是否可運作。 請注意，當您儲存排程時，最多可能需要一分鐘的時間，資料重新整理功能才會開始執行。  
  
5.  在 [最早開始時間] 中選擇下列其中一項：  
  
    1.  **[下班後]** 會指定下班之後的處理時段，此時資料庫伺服器很有可能已經收集到整個工作日所產生的最新資料。  
  
    2.  **[特定最早開始時間]** 是將資料重新整理要求加入處理佇列當日最早的時分。 您可以用 15 分鐘的間隔指定分鐘。 此設定會套用到目前日期及未來日期。 例如，如果您指定的值為早上 6 點 30 分， 而目前時間為下午 4 點 30 分，重新整理要求將會加入目前日期的佇列，因為下午 4 點 30 分 在早上 6 點 30 分之後。  
  
     [最早開始時間] 定義要求加入處理佇列的時間。 實際的處理會發生於伺服器有足夠的資源開始資料處理。 在處理完成後，就會將實際處理時間記錄在資料重新整理記錄中。  
  
6.  選取 **[並且盡快重新整理]** 核取方塊，以便在伺服器可以處理資料重新整理時，盡快執行。 成功的資料重新整理作業結果會確認資料來源可以使用，而且權限和伺服器組態的設定正確。  
  
7.  在 [電子郵件通知] 中，輸入發生處理錯誤時要通知之人員的電子郵件地址。  
  
8.  在 [認證] 中，指定用來執行資料重新整理作業的帳戶。 此帳戶必須在活頁簿上具有「參與」權限，讓它可以開啟活頁簿來重新整理其資料。 它必須是 Windows 網域使用者帳戶。 在許多情況下，此帳戶也必須擁有資料重新整理期間所使用之外部資料來源的讀取權限。 具體地說，如果您原本使用 [使用 Windows 驗證] 選項匯入資料，則會建立連接字串來使用目前使用者的 Windows 認證。 如果目前的使用者是資料重新整理帳戶，該帳戶必須擁有外部資料來源的讀取權限，資料重新整理才會成功。 選擇下列其中一個選項：  
  
    1.  選擇 **[使用系統管理員設定的資料重新整理帳戶]** 來使用 PowerPivot 自動資料重新整理帳戶處理資料重新整理作業。  
  
    2.  如果您想要輸入使用者名稱和密碼，選擇 **[使用下列 Windows 使用者認證連接]** 。 請以 domain\user 的格式輸入帳戶資訊。  
  
    3.  如果您知道目標應用程式的識別碼 (其中包含您要使用之先前儲存的認證)，選擇 **[使用儲存在 Secure Store Service 中的認證連接]** 。  
  
     如需這些選項的詳細資訊，請參閱[PowerPivot 資料重新整理設定的預存認證&#40;PowerPivot for SharePoint&#41; ](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)並[設定 PowerPivot 無人看管資料重新整理帳戶&#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
9. 如果您要資料重新整理重新查詢所有的原始資料來源，則選取 [資料來源] 中的 **[所有資料來源]** 核取方塊。  
  
     如果您選取這個選項，提供 PowerPivot 資料的任何外部資料來源都會自動包含在重新整理中，即使隨著您加入或移除提供資料給活頁簿的資料來源，而使得資料來源清單經過一段時間後已變更也是如此。  
  
     如果您要以手動方式選取要併入處理的資料來源，請清除 **[所有資料來源]** 核取方塊。 如果您稍後會加入新資料來源以修改活頁簿，請務必更新排程中的資料來源清單。 否則，較新的資料來源將不會包含在重新整理作業中。  
  
     您可以選擇的資料來源清單是在開啟活頁簿的 [管理 PowerPivot 資料重新整理] 頁面時，從 PowerPivot 活頁簿擷取的。  
  
     請務必只選取符合下列準則的資料來源：  
  
    -   資料來源必須可在執行資料重新整理時使用，並且也可在指定的位置使用。 如果原始資料來源是位於撰寫活頁簿之人員的本機磁碟機上，則必須從資料重新整理作業排除該資料來源，或設法將該資料來源發行到可透過網路連接存取的位置。 如果您將資料來源移至某個網路位置，請務必在 [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 中開啟活頁簿，並更新資料來源連接資訊。 這是重新建立儲存在 PowerPivot 活頁簿的連接資訊所必須執行的動作。  
  
    -   您必須使用內嵌在 PowerPivot 活頁簿或是在排程中指定的認證資訊，來存取資料來源。 當您使用 PowerPivot for Excel 匯入資料時，會在 PowerPivot 活頁簿中儲存內嵌的認證資訊。 內嵌的認證資訊通常是 SSPI=IntegratedSecurity 或 SSPI=TrustedConnection，表示使用目前使用者的認證連接到資料來源。 如果您要覆寫資料重新整理排程中的認證資訊，可以指定預先定義的預存認證。 如需詳細資訊，請參閱 < [PowerPivot 資料重新整理設定的預存認證&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
    -   您指定的所有資料來源的都必須能夠順利執行資料重新整理。 否則，這項作業會捨棄重新整理的資料，僅保留活頁簿最後儲存的版本。 請排除任何您不確定的資料來源。  
  
    -   資料重新整理必須不能使活頁簿中的其他資料失效。 當您重新整理資料子集時，請務必了解一旦較新的資料與不是來自相同時間週期的靜態資料彙總後，活頁簿是否仍然為有效。 身為活頁簿的作者，您必須知道資料的相依性，並確定資料重新整理是否適用於活頁簿本身。  
  
10. 您可以選擇性地定義特定資料來源的個別排程。 這對於您將原始資料來源設定成按照排程自行更新非常有用。 例如，如果 PowerPivot 資料來源使用的資料，是來自每週一凌晨 02:00 會重新整理的資料超市，則可以為資料超市定義內嵌排程，以便在每週一的凌晨 04:00 擷取其重新整理的資料。  
  
11. 按一下 **[確定]** 以儲存排程。  
  
##  <a name="drverify"></a> 確認資料重新整理  
 確認資料重新整理最好的方式，就是立即執行資料重新整理，然後檢閱記錄頁面來查看是否成功完成。 選取排程上的 **[並且盡快重新整理]** 核取方塊將會提供資料重新整理可以運作的驗證。  
  
 您可以在活頁簿的 [資料重新整理記錄] 頁面中，檢視資料重新整理作業的目前和過去記錄。 這個頁面只有在已經為活頁簿排程資料重新整理才會出現。 如果沒有任何資料重新整理排程，就會改出現排程定義頁面。  
  
 您必須擁有「參與」權限或更大的權限，才能檢視資料重新整理記錄。  
  
1.  在 SharePoint 網站上，開啟包含 PowerPivot 活頁簿的文件庫。  
  
     沒有任何視覺指標，可識別在 SharePoint 文件庫中的哪個活頁簿包含 PowerPivot 資料。 您必須事先知道哪個活頁簿包含可重新整理的 PowerPivot 資料。  
  
2.  選取文件，然後按一下出現在右邊的向下箭號。  
  
3.  選取 **[管理 PowerPivot 資料重新整理]**。  
  
 隨即顯示記錄頁面，以顯示在目前 Excel 活頁簿中為 PowerPivot 資料顯示所有重新整理活動的完整記錄，包含最近的資料重新整理作業狀態。  
  
 在某些情況下，您可能會看到實際的處理時間，與您指定的時間並不同。 如果在伺服器上處理負載繁重，就會發生這樣的情況。 在繁重的負載下， [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 服務執行個體將會等到有足夠的系統資源釋放後，才開始進行資料重新整理。  
  
 在完成重新整理作業時必須簽入活頁簿。 活頁簿會在該時間隨重新整理的資料一起儲存。 如果檔案已簽出，則會略過資料重新整理，直到下一個排程時間為止。  
  
 如果您看到非預期的狀態訊息 (例如，重新整理作業失敗或已取消)，則可以檢查權限和伺服器可用性，來調查該問題。  
  
 請檢閱 TechNet WIKI 上的 PowerPivot 資料重新整理疑難排解頁面，以取得解決資料重新整理問題的協助。 如需詳細資訊，請參閱 [PowerPivot 資料重新整理疑難排解](https://go.microsoft.com/fwlink/?LinkId=251594)。  
  
> [!NOTE]  
>  SharePoint 管理員可以透過在管理中心的 PowerPivot 管理儀表板中檢視合併的資料重新整理報表來協助您疑難排解資料重新整理問題。 如需詳細資訊，請參閱＜ [PowerPivot Management Dashboard and Usage Data](power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [與 SharePoint 2010 的 PowerPivot 資料重新整理](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [檢視資料重新整理記錄&#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)   
 [設定 PowerPivot 資料重新整理的預存的認證&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
