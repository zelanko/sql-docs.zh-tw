---
title: 建立及設定 Power Pivot 服務應用程式，在 CA |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 581bcc4777121d42b8f7e6b629d98e26b49b425d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-configure-power-pivot-service-application-in-ca"></a>建立及設定 Power Pivot 服務應用程式，在 CA 中
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務的共用服務執行個體。 每一個服務應用程式都有它自己的應用程式識別、組態設定、屬性以及內部資料儲存位置。  
  
 本主題包含下列幾節：  
  
 [決定是否要建立新的 Power Pivot 服務應用程式](#determine)  
  
 [建立 Power Pivot 服務應用程式](#CreateApp)  
  
 [設定 Power Pivot 服務應用程式](#ConfigApp)  
  
 [將 Power Pivot 服務應用程式指派給 Web 應用程式](#AssignGSA)  
  
 [編輯服務應用程式屬性](#EditGSA)  
  
##  <a name="determine"></a> 決定是否要建立新的 Power Pivot 服務應用程式  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝在伺服器陣列中必須至少有一個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 如果您使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具來設定伺服器，就會自動建立服務應用程式。 否則，您必須在管理中心手動建立 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。  
  
 建立服務應用程式可讓服務變成可用，並產生服務應用程式資料庫。 根據您在建立服務應用程式時所選取的選項而定，會將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務連接加入預設的服務連接群組。 所有訂閱預設服務連接群組的 SharePoint Web 應用程式，都會立即自動取得 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的存取權。  
  
 您可以建立多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 雖然一個服務應用程式就足以應付大部分的部署狀況，但是如果您有下列商務需求，即可考慮建立其他的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式：  
  
-   針對每一個應用程式，使用不同的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管資料重新整理帳戶。  
  
-   使用不同的逾時、使用量記錄和臨界值來進行查詢回覆報告。  
  
-   將服務管理委派給不同的人。 系統管理員只會看到他所管理之應用程式的資料重新整理記錄、使用量資料和其他屬性。 如果您需要隔離 SharePoint Web 應用程式 (例如，如果您的公司是一種主機服務，必須確保針對屬於不同客戶的 SharePoint Web 應用程式進行資料隔離)，則建立個別的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式有助於符合隔離需求，方法是確保每一位服務管理員只會看到其所管理之應用程式的組態設定和屬性。  
  
 建立其他服務應用程式會引進管理服務關聯的新需求。 也就是說，它會要求您針對您所建立的每一個額外服務應用程式來建立及使用自訂服務關聯清單。  
  
 如果您沒有建立其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的特定理由，則應該為伺服器陣列中的所有 Web 應用程式，使用單一服務應用程式。  
  
##  <a name="CreateApp"></a> 建立 Power Pivot 服務應用程式  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  在 **[服務應用程式]** 功能區中，按一下 **[新增]**。  
  
3.  選取 [SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式]。 如果它沒有出現在清單中，表示 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 未安裝或未正確設定。  
  
4.  在 [建立新的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式] 頁面中，輸入應用程式的名稱。 預設值是 PowerPivotServiceApplication\<數 >。 如果您要建立多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，描述性名稱將可協助其他系統管理員，了解如何使用應用程式。  
  
5.  在 [應用程式集區] 中，針對此應用程式建立新的應用程式集區 (建議作法)。 請針對此應用程式集區選取或建立受管理的帳戶。 請務必指定網域使用者帳戶。 網域使用者帳戶會啟用 SharePoint 的受管理帳戶功能，好讓您在一個地方更新密碼和帳戶資訊。 如果您計劃將部署向外延展，以包括將在相同識別下執行的其他服務執行個體，也需要網域帳戶。  
  
6.  在 **[資料庫伺服器]** 中，預設值是主控伺服陣列組態資料庫的 SQL Server Database Engine 執行個體。 您可以使用這部伺服器，或選擇不同的 SQL Server。  
  
7.  在**資料庫名稱**，預設值是 Powerpivotserviceapplication1_<guid>\<guid >。 您必須針對每個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式建立唯一的資料庫。 預設的資料庫名稱會對應至服務應用程式的預設名稱。 如果您輸入唯一的服務應用程式名稱，請依照類似的命名慣例來命名資料庫名稱，以利同時管理它們。  
  
8.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 **[SQL 驗證]**，請參考 SharePoint 管理員指南，以了解有關如何在 SharePoint 部署中使用這個驗證類型的最佳作法。  
  
9. 您也可以選擇性地選取 [將這個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的 Proxy 加入到伺服器陣列的預設 Proxy 群組] 核取方塊。 這會將服務應用程式連接加入到預設的服務連接群組。  
  
     如果您正在建立第一個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，就必須選取這個核取方塊。 預設連接群組中必須有一個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，才能讓 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板正常運作。  
  
     請勿將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式加入到預設連接群組 (如果已有這類服務應用程式存在)。 加入相同服務應用程式類型的多個項目並不是支援的組態，而且可能會發生錯誤。 如果您要建立其他服務應用程式，請將此應用程式加入到自訂清單，而不要加入到預設連接群組。  
  
     如需服務關聯的詳細資訊，請參閱 [在管理中心將 Power Pivot 服務應用程式連接到 SharePoint Web 應用程式](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)。  
  
10. 按一下 **[確定]**。 此服務將會與伺服器陣列服務應用程式清單中的其他受管理的服務一起顯示。  
  
##  <a name="ConfigApp"></a> 設定 Power Pivot 服務應用程式  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式是使用預設組態所建立。 在大部分的情況下建議使用預設值。 只有在您遇到回應時間變慢或已捨棄連接時，或是如果您要改變特定 SharePoint Web 應用程式的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務組態時，才變更它們。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
     在服務應用程式的清單中，您應該會看到剛才建立和命名的服務應用程式。 預設值是 **[PowerPivotServiceApplication1]**。  
  
2.  按一下 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 隨即開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板。  
  
3.  在儀表板右上角的 **[動作]** 清單中，按一下 **[設定服務應用程式設定]**。  
  
4.  在 [資料庫載入逾時] 中，提高或降低值，以變更 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務等待轉送載入資料要求至 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 執行個體時，該執行個體回應的時間長度。 因為非常大型的資料集需要一些時間透過傳輸來移動，所以您必須允許 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體有足夠的時間來擷取 Excel 活頁簿，並將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料移到 Analysis Services 執行個體，以進行查詢處理。 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料可能非常大，因此預設值為 30 分鐘。  
  
5.  在 **[連接集區逾時]** 中增加或減少值，以變更閒置的資料連接持續開啟的分鐘數。 預設值為 30 分鐘。 在這段期間， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務將針對來自相同 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料之相同 SharePoint 使用者的唯讀要求，重複使用閒置資料連接。 如果在指定的期間內沒有收到該資料的進一步要求，將會從集區移除該連接。 有效值為 1 到 3600 秒。 如需連接集區的詳細資訊，請參閱[組態設定參考 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)。  
  
6.  在 [最大使用者連接集區大小] 中，提高或降低值，以變更 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務將為每個 SharePoint 使用者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料集和版本組合建立個別連接集區的最大閒置連接數。  
  
     預設值是 1000 個閒置連接。 有效值為 -1 (無限制)、0 (停用使用者連接共用)，或 1 至 10000。  
  
     這些連接集區可讓服務以更有效率的方式支援由相同使用者連至相同唯讀資料的持續連接。 如果您停用連接共用，將會重新建立每一個連接。  
  
     請注意，變更連接集區大小的限制 (包括將它設定為 0) 將不會導致卸除連接。 連接集區存在的目的是為了減少連接到資料的等候時間。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務永遠都不會拒絕以連接集區設定為基礎的連接。  
  
7.  在 [最大管理連接集區大小] 中，提高或降低值，以變更針對連至 Analysis Services 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務連接所建立之連接集區中開啟的連接數。 每個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體都會在相同的電腦上開啟 Analysis Services 執行個體的個別管理連接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務會建立不同的集區，以便基於檢查閒置連接和監視伺服器健全狀況的目的重複使用管理連接。 預設值是 200 個連接。 有效值為 -1 (無限制)、0 (停用管理連接共用) 或 1 到 10000。 如果您選取 0，將會重新建立每一個連接。  
  
8.  在 [配置方法] 中，您可以指定負載平衡結構描述， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務會使用該結構描述來選取特定的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，針對初始要求進行負載平衡處理。 預設值為 **[依據健全狀態]**，根據伺服器狀態來配置要求，這是以可用的記憶體及處理器使用量來衡量。 或者，您可以選擇 **[循環配置資源]** ，以相同的重複順序將要求配置到伺服器，而不論伺服器是忙碌或閒置。  
  
9. 在 [資料重新整理] 的 **[上班時間]** 中，您可以指定定義上班時間的小時範圍。 資料重新整理排程可以在下班後執行，以取得在正常上班時間所產生的交易資料。  
  
10. 您可以在 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管的資料重新整理帳戶] 中指定預先定義的 Secure Store Service 目標應用程式，它會儲存預先定義的帳戶來執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料重新整理作業。 請務必指定目標應用程式名稱，而非識別碼。 如果您在 SQL Server 安裝程式中使用 [新的伺服器] 選項來安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，就會自動建立自動資料整理的目標應用程式。 否則，您必須手動建立目標應用程式。 如需如何設定帳戶的相關指示，請參閱 [設定 PowerPivot 無人看管的資料重新整理帳戶 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)。  
  
11. 在 **[允許使用者輸入自訂的 Windows 認證]** 中，您可以選取或清除可指定排程擁有者是否可以輸入任意 Windows 認證來執行資料重新整理排程的核取方塊。 如果您選取這個核取方塊， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式將針對每組預存認證建立及管理目標應用程式。 如需詳細資訊，請參閱 [設定 Power Pivot 資料重新整理的預存認證 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)。  
  
12. 在 **[最大處理記錄長度]** 中，您可以指定要保留資料重新整理處理的記錄多久。 此資訊會出現在資料重新整理記錄頁面中，這些頁面會針對使用資料重新整理的每個活頁簿而保留。 此資訊也會出現在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中。  
  
13. 在 [使用量資料收集] 的 **[查詢報告間隔]** 中，指定報告查詢統計資料的間隔時間。 查詢統計資料會報告成單一事件，以最小化伺服器對伺服器的通訊。  
  
14. 在 [使用量資料記錄] 中，指定保留使用量資料歷程記錄的時間長度。 使用量資訊會出現在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中。 如果您為使用量資料記錄指定的值太低，報表將會比較沒有效率。  
  
15. 在 [使用量資料收集] 的每個查詢回應臨界值中，指定可決定某個類別目錄停止且另一個類別目錄開始的上限。 這些類別目錄會建立要針對哪一個查詢行為計算的基準。 您可以使用這些類別目錄來監視系統的查詢回應時間趨勢。 此資訊會出現在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中。  
  
16. 按一下 **[確定]** 儲存您的變更。  
  
     對載入逾時或配置方法的變更只會套用至新的內送要求。 已在進行中的要求受限於接收要求時生效的值。  
  
##  <a name="AssignGSA"></a> 將 Power Pivot 服務應用程式指派給 Web 應用程式  
 設定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式之後，即可將它指派給 Web 應用程式，方法是將它加入到該 Web 應用程式的服務應用程式連接清單。 有兩種方式可以執行此動作：  
  
-   將它加入 **預設** 連接群組。 *「預設連接群組」* (Default Connection Group) 是服務應用程式連接的集合，可供任何參考它的 Web 應用程式使用。 您必須將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式加入到這個清單。  
  
-   為特定的 Web 應用程式建立 **[自訂]** 連接清單。 如果您建立了多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，則可在自訂清單中選取要使用哪一個。  
  
 預設的連接群組將可接受相同類型的多個服務應用程式。 不過請注意，將一個以上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式加入到這個清單並不是支援的組態。  
  
1.  在 [管理中心] 的 **[應用程式管理]** 中，按一下 **[管理 Web 應用程式]**。  
  
2.  選取您要指派連接的應用程式 (例如 SharePoint-80)。  
  
3.  按一下 **[服務連接]**。  
  
4.  在 [Edit the following group of associations (編輯下列關聯群組)] 中，選取 **default** 或 **[custom]**。  
  
5.  若是 **[custom]**，請選取您想要使用的每個服務應用程式連接旁邊的核取方塊。 如果您具有多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式 (由設為 [Power Pivot 服務應用程式 Proxy] 的類型指出)，請務必只選擇一個。  
  
6.  按一下 **[確定]**。  
  
##  <a name="EditGSA"></a> 編輯服務應用程式屬性  
 使用下列指示來重新開啟屬性頁，以指定服務的應用程式名稱、應用程式集區、資料庫設定以及服務關聯。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  選取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，但是不要在上面按一下。 您可以按一下類型名稱來選取整列。  
  
3.  在功能區上按一下 **[屬性]** 。  
  
## <a name="see-also"></a>另請參閱  
 [管理中心的 Power Pivot 伺服器管理和設定](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
