---
title: 設定 SQL Server 的使用方式和診斷資料收集 (CEIP) | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: configuration
ms.openlocfilehash: 44a8d6c22d7dd003f7c6e90963eb546e6ca1bf50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65372762"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-ceip"></a>設定 SQL Server 的使用狀況和診斷資料收集 (CEIP)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="summary"></a>摘要

根據預設，Microsoft SQL Server 會收集客戶如何使用應用程式的相關資訊。 具體來說，SQL Server 會收集有關安裝體驗、使用情況和效能的相關資訊。 這些資訊可協助 Microsoft 改善產品，以進一步滿足客戶需求。 例如，Microsoft 會收集客戶所遇到之錯誤代碼的相關資訊，以便修正相關錯誤、改善如何使用 SQL Server 的相關文件，以及判斷是否應將功能加入到產品中以滿足客戶。

具體來說，Microsoft 不會透過此機制傳送下列類型的資訊：
- 使用者資料表內的任何值
- 任何登入認證或其他驗證資訊
- 個人識別資訊 (PII)

下列範例案例包含可協助改善產品的功能使用方式資訊。

SQL Server 2017 支援資料行存放區索引，以便快速分析案例。 資料行存放區索引針對新插入的資料會使用傳統的「B 型樹狀結構」索引結構，並結合特殊的資料行導向壓縮結構以壓縮資料並提升查詢執行的速度。 產品包含啟發學習法以在背景中將資料從 B 型樹狀結構移轉至壓縮結構，因此得以加快未來的查詢結果。

如果背景作業跟不上插入資料的速率，則查詢效能可能會比預期還要慢。 為了改善產品，Microsoft 會收集有關 SQL Server 跟上自動資料壓縮程序之情況的資訊。 產品小組會使用此資訊來微調執行壓縮之程式碼的頻率和並行性。 此查詢偶爾會運行來收集這項資訊，以便我們 (Microsoft) 可以評估資料移動速率。 這有助於最佳化產品的啟發學習法。  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

請注意，此程序著重於為客戶提供價值的必要機制。 產品小組不會查看索引中的資料，或將該資料傳送給 Microsoft。 SQL Server 2017 一律會收集並傳送與安裝程序中安裝體驗相關的資訊，以便我們能夠快速找出並修正客戶所遇到的任何安裝問題。 SQL Server 2017 可以透過下列機制設定為不傳送資訊 (針對每個伺服器執行個體) 給 Microsoft：
- 透過使用 [錯誤和使用方式報表] 應用程式
- 透過在伺服器上設定登錄子機碼

針對 Linux 上的 SQL Server，請參閱 [Linux 上的 SQL Server 客戶意見反應](https://docs.microsoft.com/sql/linux/sql-server-linux-customer-feedback) \(英文\)

> [!NOTE]
> 您僅可在付費版本的 SQL Server 中停用將資訊傳送給 Microsoft 的功能。

## <a name="remarks"></a>Remarks
 - 不支援移除或停用 SQL CEIP 服務。 
 - 不支援從叢集群組移除 SQL CEIP 資源。 

若要退出資料收集，請參閱[開啟或關閉本機稽核](usage-and-diagnostic-data-in-local-audit.md#turning-local-audit-on-or-off)

## <a name="error-and-usage-reporting-application"></a>[錯誤和使用方式報表] 應用程式 

安裝後，可以透過 [錯誤和使用方式報告] 應用程式變更 SQL Server 元件和執行個體的使用方式和診斷資料收集設定。 此應用程式包含在 SQL Server 安裝之中。 此工具可讓每個 SQL Server 執行個體設定自己的 [使用方式報表] 設定。

> [!NOTE]
> [錯誤和使用方式報表] 應用程式會列出於 SQL Server 的 [組態工具] 底下。 您可以利用與 SQL Server 2017 中相同的方式，使用此工具管理您的「錯誤報告」和「使用方式和診斷資料」收集的喜好設定。 「錯誤報告」有別於「使用方式和診斷資料」收集，因此可以獨立於「使用方式和診斷資料」收集進行開啟或關閉。 「錯誤報告」會收集要傳送給 Microsoft 的損毀傾印，其中可能包含[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)中所述的機密資訊。

若要啟動 [SQL Server 錯誤和使用方式報表]，請按一下或點選 [開始]  ，然後在搜尋方塊中搜尋「錯誤」。 隨即顯示 [SQL Server 錯誤和使用方式報表] 項目。 啟動工具之後，您可以管理針對該電腦上所安裝之執行個體和元件所收集的使用方式和診斷資料及嚴重錯誤。

針對付費版本，請使用 [使用方式報表] 核取方塊來管理將使用方式和診斷資料傳送到 Microsoft 的功能。

針對付費或免費版本，請使用 [錯誤報告] 核取方塊來管理將嚴重錯誤及損毀傾印的意見反應傳送到 Microsoft 的功能。

## <a name="set-registry-subkeys-on-the-server"></a>在伺服器上設定登錄子機碼

企業客戶可以設定群組原則設定，來選擇加入或退出使用方式和診斷資料收集。 這是透過設定以登錄為基礎的原則來完成。 相關的登錄子機碼與設定如下：

- 針對 SQL Server 執行個體功能：
    
    子機碼 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    登錄項目名稱 = CustomerFeedback
    
    項目類型 DWORD：0 為退出；1 為加入
    
    {InstanceID} 是指執行個體類型和執行個體，如下列範例所示：

    - MSSQL14.CANBERRA 適用於搭配 SQL Server 2017 Database 引擎及 "CANBERRA" 執行個體名稱的情況
    - MSAS14.CANBERRA 適用於搭配 SQL Server 2017 Analysis Services 及 "CANBERRA" 執行個體名稱的情況
    - MSRS14.CANBERRA 適用於搭配 SQL Server 2017 Reporting Services 及 "CANBERRA" 執行個體名稱的情況

- 針對所有共用功能：
    
    子機碼 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}
    
    登錄項目名稱 = CustomerFeedback
    
    項目類型 DWORD：0 為退出；1 為加入

> [!NOTE]
> {Major Version} 是指 SQL Server 版本。例如，140 指的是 SQL Server 2017

- 對於 SQL Server Management Studio 17 和 SQL Server Management Studio 18，請參閱 [SQL Server Management Studio 中的使用者協助](../ssms/sql-server-management-studio-telemetry-ssms.md)

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>設定損毀傾印收集的登錄子機碼

類似於舊版 SQL Server 中的行為，使用 SQL Server 2017 Enterprise 的客戶可以在伺服器上設定群組原則設定，來選擇加入或退出損毀傾印收集。 這是透過設定以登錄為基礎的原則來完成。 相關的登錄子機碼與設定如下： 

- 針對 SQL Server 執行個體功能：

    子機碼 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    RegEntry 名稱 = EnableErrorReporting

    項目類型 DWORD：0 為退出；1 為加入
 
    {InstanceID} 是指執行個體類型和執行個體，如下列範例所示： 

    - MSSQL14.CANBERRA 適用於搭配 SQL Server 2017 Database 引擎及 "CANBERRA" 執行個體名稱的情況
    - MSAS14.CANBERRA 適用於搭配 SQL Server 2017 Analysis Services 及 "CANBERRA" 執行個體名稱的情況
    - MSRS14.CANBERRA 適用於搭配 SQL Server 2017 Reporting Services 及 "CANBERRA" 執行個體名稱的情況
 

- 針對所有共用功能：
    
    子機碼 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}

    RegEntry 名稱 = EnableErrorReporting

    項目類型 DWORD：0 為退出；1 為加入

> [!NOTE]
> {Major Version} 是指 SQL Server 版本。 例如，"140" 指的是 SQL Server 2017。

SQL Server 2017 損毀傾印收集會接受這些登錄子機碼上以登錄為基礎的群組原則。 

## <a name="crash-dump-collection-for-ssms"></a>SSMS 的損毀傾印收集
SSMS 不會收集自己的損毀傾印。 與 SSMS 相關的任何損毀傾印，都會以 Windows 錯誤報告之一部分的方式收集。

開啟或關閉這項功能的程序會依作業系統版本而異。 若要開啟或關閉功能，請遵循適用於您 Windows 版本之適當文件中的步驟。
 
- Windows Server 2016 與 Windows 10

    [在組織中設定 Windows 診斷資料](https://docs.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)
- Windows Server 2008 R2 與 Windows 7

    [WER 設定](/windows/desktop/wer/wer-settings) \(英文\)
 
## <a name="feedback-for-analysis-services"></a>針對 Analysis Services 的意見反應

在安裝期間，SQL Server 2016 Analysis Services 會將特殊帳戶加入至您的 Analysis Services 執行個體。 此帳戶是 Analysis Services 伺服器系統管理員角色的成員。 此帳戶是用來從 Analysis Services 執行個體針對意見反應收集資訊。  

您可以將服務設定為不傳送使用方式和診斷資料，如＜在伺服器上設定登錄子機碼＞一節中所述。 不過，這麼做並不會移除該服務帳戶。 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
