---
title: Set-powerpivotserviceapplication 指令程式 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a0951f53451141ead27cc3d7aa5f1346dbb47694
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Set-PowerPivotServiceApplication 指令程式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  設定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的屬性。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Set-PowerPivotServiceApplication Cmdlet 會更新伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的屬性。 Identity 是必要參數。 您必須提供要更新屬性之服務應用程式的 GUID。  
  
 若要確認您的變更，執行下列指令程式： Get-powerpivotserviceapplication-Identity \<GUID > | 格式清單。  
  
## <a name="parameters"></a>參數  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>識別\<SPGeminiServiceApplicationPipeBind >  
 指定要更新的服務應用程式。 此類型必須是有效 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式物件的有效 GUID 或執行個體。 您可以使用 Get-PowerPivotServiceApplication 傳回物件的執行個體。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<int >  
 指定為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務與 Analysis Services 之間的連接所建立之連接集區中的開啟連接數目。 每個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體都會在相同的電腦上開啟 Analysis Services 執行個體的個別管理連接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務會建立不同的集區，以便基於檢查閒置連接和監視伺服器健全狀況的目的重複使用管理連接。 預設值是 200 個連接。 有效值為 -1 (無限制)、0 (停用管理連接共用) 或 1 到 10000。 如果您選取 0，將會重新建立每一個連接。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|200|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<SwitchParameter>]  
 指定排程擁有者是否可以輸入任意 Windows 認證來執行資料重新整理排程。 如果您選取這個核取方塊， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式將會針對每組預存認證來建立及管理目標應用程式。 預設設為 true。 若要關閉此功能，請設定 AllowCustomWindowsCredentials:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime\<字串 >  
 指定定義營業日之時數範圍的結束點。 資料重新整理排程可以在下班後執行，以取得在正常上班時間所產生的交易資料。 預設值是下午 8:00。  用引號括住有效值，亦即 12 小時制，上午 或下午 (例如，"08:00PM")。 小時必須介於 1 到 12 之間。 分鐘必須介於 1 到 59 之間。  
  
 若要指定營業日的完整時數範圍，您必須同時設定 BusinessHoursStartTime 和 BusinessHoursEndTime。 這兩個參數定義構成營業日的時數間隔。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|8 PM|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime \<string>  
 指定定義營業日之時數範圍的開始點。 資料重新整理排程可以在下班後執行，以取得在正常上班時間所產生的交易資料。 預設值是上午 4:00。  用引號括住有效值，亦即 12 小時制，上午 或下午 (例如，"04:00AM")。 小時必須介於 1 到 12 之間。 分鐘必須介於 1 到 59 之間。  
  
 若要指定營業日的完整時數範圍，您必須同時設定 BusinessHoursStartTime 和 BusinessHoursEndTime。 這兩個參數定義構成營業日的時數間隔。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|4 AM|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<int >  
 指定非使用中資料庫在從記憶體卸載之後保留在檔案系統中的時數。 預設值為 120 小時。 清除作業會使用這個設定來判斷要刪除的檔案。 未有任何活動達 168 小時 (記憶體中 48 小時，快取中 120 小時) 的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫都會透過清除作業，從磁碟中刪除。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|120|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-confirm-switch"></a>確認\<切換 >  
 在執行命令之前提示您確認。 此值預設是啟用的。 若要在命令中略過確認回應，請在命令上指定 Confirm:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-connectionpoolsize-int"></a>-ConnectionPoolSize \<int>  
 在用於每個 SharePoint 使用者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料集和版本組合的個別連接集區中，指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務將建立的閒置連接數上限。 預設值是 1000 個閒置連接。 有效值為 -1 (無限制)、0 (停用使用者連接共用)，或 1 至 10000。 這些連接集區可讓服務以更有效率的方式支援由相同使用者連至相同唯讀資料的持續連接。 如果您停用連接共用，將會重新建立每一個連接。 請注意，變更連接集區大小的限制 (包括將它設定為 0) 將不會導致卸除連接。 連接集區存在的目的是為了減少連接到資料的等候時間。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務永遠都不會拒絕以連接集區設定為基礎的連接。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|1000|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<int>  
 指定閒置資料連接將維持開啟狀態多少分鐘。 預設值為 1800 秒 (30 分鐘)。 在這段期間， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式將會針對來自相同 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料之相同 SharePoint 使用者的唯讀要求，重複使用閒置資料連接。 如果在指定的期間內沒有收到該資料的進一步要求，將會從集區移除該連接。 有效值為 1 到 3600 秒。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|1800|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<int >  
 指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式在轉送載入資料要求至 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 執行個體時，等待該執行個體回應的時間長度。 因為非常大型的資料集需要一些時間透過傳輸來移動，所以您必須允許 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體有足夠的時間來擷取 Excel 活頁簿，並將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料移到 Analysis Services 執行個體，以進行查詢處理。 預設值為 1800 秒 (30 分鐘)。 有效值的範圍從 1 到 3600 秒。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|1800|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<int >  
 指定停用排程之前的連續失敗次數。 預設值是 10。 您也可以輸入 0，絕不因為重新整理失敗而停用排程。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|10|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<int>  
 指定停用排程之前的資料重新整理循環數目，或輸入 0，絕不因為未有任何活動而停用排程。 預設值是 10 個循環。  
  
 活頁簿未有任何活動是以多個資料重新整理週期沒有連接事件來表示。 無論作業成功或失敗，每次觸發資料重新整理作業 (透過排程或 [立即執行] 作業) 時，都會計算資料重新整理週期。 如果週期數目通過 (預設為 10)，而且沒有活頁簿的連接要求，資料重新整理排程則會因為未有任何活動而停用。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|10|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<int>  
 指定要保留資料重新整理處理之歷程記錄的天數。 此資訊會出現在資料重新整理記錄頁面中，這些頁面會針對使用資料重新整理的每個活頁簿而保留。 此資訊也會出現在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中。 預設值為 365 天。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|365|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation\<切換 >  
 指定以健全狀況為基礎的配置演算法，將連接要求轉送至具有最多可用 CPU 或記憶體資源的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器。 這是預設配置演算法。 HealthBasedAllocation 和 RoundRobinBasedAllocation 互斥。 您必須指定其中一項。 如果同時將兩者設為 false，則會使用 HealthBasedAllocation，因為它是預設值。 如果同時將兩者設為 true，則會發生驗證錯誤。 這些參數的語法包含只輸入參數名稱，或輸入 parameter:$true 或 parameter:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<int >  
 指定要計算載入和連接事件數目的間隔 (小時)，以計算負載與連接比率。 根據預設，系統每 4 小時會計算一次新比率。 有效值為 1 到 24。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|4|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<int >  
 指定載入事件與連接事件比率，做為伺服器健全狀況的指標。 預設值是百分之 20。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|20|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>-MemoryDatabaseHoldLimit \<int >  
 指定非使用中資料庫要保留在記憶體中的時數，以服務該資料的新要求。 只要您要查詢使用中的資料庫，該資料庫就會永遠保留在記憶體中，但在資料庫不再處於使用中狀態時，系統會將該資料庫另外保留在記憶體中一段時間，以防有該資料的其他要求。 預設值為 48 小時。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|48|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<int >  
 指定在將查詢報告為使用量事件之前，收集查詢回應統計資料的秒數。 預設值是 300 秒。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|300|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-roundrobinallocation-switch"></a>-RoundRobinAllocation\<切換 >  
 指定以循環配置為基礎的配置演算法，不論伺服器負載，將連接要求轉送至下一部 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器，在可用伺服器之間平均輪替要求。 HealthBasedAllocation 和 RoundRobinBasedAllocation 互斥。 您必須指定其中一項。 如果同時將兩者設為 false，則會使用 HealthBasedAllocation，因為它是預設值。 如果同時將兩者設為 true，則會發生驗證錯誤。 這些參數的語法包含只輸入參數名稱，或輸入 parameter:$true 或 parameter:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount\<字串 >  
 指定 Secure Store Service 應用程式的目標應用程式名稱，它會儲存預先定義的帳戶來執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料重新整理作業。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<int >  
 指定要保留使用量資料和伺服器健全狀況統計資料記錄的天數。 預設值為 365 天。 將此值設為 0 將會無限期地保留所有記錄。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|365|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<int >  
 設定會定義預期要求-回應交換的上限。 預設值為 3000 毫秒。 就報告用途而言，任何介於 1000 到 3000 毫秒之間完成的要求都視為預期回應。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|3000|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<int >  
 設定會定義長時間執行要求-回應交換的上限。  上限為 10000 毫秒。 任何超過此上限的要求，都會歸類到沒有上限臨界值的「已超過」類別目錄。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|10000|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<int >  
 設定會定義快速要求-回應交換的上限。 預設為 1000 毫秒。 就報告用途而言，任何介於 500 到 1000 毫秒之間完成的要求都視為快速回應。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|1000|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<int >  
 指定因時間太短而不被視為資料收集相關的回應時間類別目錄。 大多數屬於此類別目錄的回應都是伺服器對伺服器通訊。 根據預設，此值為 500 毫秒。 任何介於 0 到 500 毫秒之間完成的要求都是簡單式要求，報告用途會加以忽略。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|500|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<int>  
 指定觸發 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中報表所用之資料檔案重新整理失敗警告的臨界值 (天)。 根據預設，系統會每日更新使用量資料。 系統管理報表的資料來源 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Management Dashboard.xlsx 檔案也會依照相同的排程重新整理。 如果幾天都未更新 .xlsx 檔案，就會觸發這個健全狀況規則，表示檔案已過期。 預設值為 5 天。 有效值是 1 到 30。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|5|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 這個範例會將自動建立及管理 Secure Store Service 目標應用程式以儲存任意 Windows 認證的資料重新整理功能關閉。 它也會將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管的資料重新整理帳戶設定為預先定義的目標應用程式。  
  
 使用 Get-powerpivotserviceapplication，可取得有效識別。  
  
## <a name="example-2"></a>範例 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 這個範例指定以健全狀況為基礎的配置演算法，將連接要求轉送至具有最多可用資源的伺服器。  
  
 使用 Get-powerpivotserviceapplication，可取得有效識別。  
  
## <a name="example-3"></a>範例 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 這個範例示範如何設定營業日的起訖時間，做為排定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料重新整理的排程選項。 排程可以指定下班後選項，以便在營業日結束時執行資料重新整理。  
  
 使用 Get-powerpivotserviceapplication，可取得有效識別。  
  
  
