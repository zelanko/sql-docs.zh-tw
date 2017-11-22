---
title: "Invoke-ascmd 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2896b74a-3911-4b3f-89ab-bb375bdb34d8
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6e5d1fba56fd4cee4c736a583d8af2fe8ec6f986
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="invoke-ascmd-cmdlet"></a>Invoke-ASCmd 指令程式

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  讓資料庫管理員能夠執行 XMLA 指令碼、多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 陳述式或表格式模型指令碼語言 (TMSL) 指令碼。  
  
 在 SQL Server 2016 Analysis Services 執行個體上，只有表格式伺服器模式才支援 TMSL。  
  
 如果您想要建立資料庫或其他物件，您會使用此 Cmdlet 及指令碼輸入檔。  
  
## <a name="syntax"></a>語法  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>說明  
 Invoke-ASCmd 指令程式可以執行包含在輸入檔中的查詢或指令碼。  
  
 若是 XMLA，支援下列命令：Alter、Backup、Batch、BeginTransaction、Cancel、ClearCache、CommitTransaction、Create、Delete、DesignAggregations、Drop、Insert、Lock、MergePartitions、NotifyTableChange、Process、Restore、RollbackTransaction、Statement (用來執行 MDX 查詢和 DMX 陳述式)、Subscribe、Synchronize、Unlock、Update、UpdateCells。  
  
 若是 TMSL：Alter、Create、Delete、MergePartitions、Process、Update。  
  
 此指令程式支援 –Credential 參數，如果您設定 Analysis Services 執行個體用於 HTTP 存取，就可以使用它。 –Credential 參數會採用提供 Windows 使用者識別的 PSCredential 物件。 然後在連接到 Analysis Services 時，IIS 會模擬此使用者。 此識別必須具有 Analysis Services 執行個體的系統管理員權限，才能執行指令碼。  
  
## <a name="parameters"></a>參數  
  
### <a name="-query-string"></a>-查詢\<字串 >  
 直接在命令列上 (而不是檔案中) 指定實際指令碼、查詢或陳述式。 您也可以將查詢指定為管線輸入。 使用 **Invoke-AsCmd** 時，您必須指定 **–InputFile** 或 **–Query**參數的值。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|True (ByValue)|  
|接受萬用字元？|false|  
  
### <a name="-inputfile-string"></a>-InputFile\<字串 >  
 識別包含了 XMLA 指令碼、MDX 查詢、DMX 陳述式或 TMSL 指令碼 (JSON 中) 的檔案。 使用 **Invoke-AsCmd** 時，您必須指定 **–InputFile** 或 **–Query**參數的值。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-server-string"></a>伺服器\<字串 >  
 指定指令程式將會連接並執行的 Analysis Services 執行個體。 如果沒有提供伺服器名稱，將會建立 localhost 的連接。 若為預設執行個體，請單獨指定伺服器名稱。 若為具名執行個體，請使用格式 servername\instancename。 若為 HTTP 連接，請使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|localhost|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-database-string"></a>-資料庫\<字串 >  
 指定將會對其執行 MDX 查詢或 DMX 陳述式的資料庫。 因為資料庫名稱是內嵌在 XMLA 指令碼中，所以當指令程式執行 XMLA 指令碼時，系統會忽略資料庫參數。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 指定提供 Windows 使用者名稱和密碼的 PSCredential 物件。 僅當 Analysis Services 執行個體設定用於 HTTP 存取時 (使用基本驗證)，才指定此參數。 對於使用整合式安全性的原生連接，則會忽略此參數。  
  
 如果此參數存在，它提供的認證會附加到連接字串。 連接到 Analysis Services 時，IIS 就會模擬此使用者識別。 如果沒有指定認證，則會使用執行此工具之使用者的預設 Windows 帳戶。  
  
 若要使用此參數，請先使用 Get-Credential 來建立 PSCredential 物件，以便指定使用者名稱和密碼 (例如 `$Cred=Get-Credential “adventure-works\admin”`。 然後，您可以透過管道將這個物件傳送至 -Credential 參數 `(-Credential:$Cred`)。  
  
   如需 HTTP 存取的詳細資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|True (ByValue)|  
|接受萬用字元？|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<int >  
 指定 Analysis Services 執行個體之連接逾時之前的秒數。逾時值必須是介於 0 到 65534 之間的整數。 如果指定了 0，連線嘗試就不會逾時。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|30|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<int >  
 指定查詢逾時之前的秒數。如果沒有指定逾時值，查詢就不會逾時。逾時必須是介於 1 到 65535 之間的整數。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|30|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-variable-string"></a>-變數\<string [] >  
 指定其他指令碼變數。 每個變數都是名稱/值組。 如果此值包含內嵌空格或控制字元，就必須以雙引號括住。 您可以使用 PowerShell 陣列來指定多個變數及其值。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-tracefile-string"></a>-TraceFile\<字串 >  
 識別執行 XMLA 指令碼、MDX 查詢或 DMX 陳述式時接收 Analysis Services 追蹤事件的檔案。 如果檔案已經存在，則會自動覆寫該檔案 (但使用 -TraceLevel:Duration 和 -TraceLevel:DurationResult 參數設定所建立的追蹤檔案除外)。 包含空格的檔案名稱必須加上雙引號 (" ")。 如果檔案名稱無效，則會產生一則錯誤訊息。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat\<字串 >  
 為 -TraceFile 參數指定檔案格式 (如果指定了這個參數的話)。 可用的選項為 text 或 csv。 預設值是 "csv"。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|csv|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter\<字串 >  
 在您將 csv 指定為追蹤檔案格式時，指定要當做追蹤檔案分隔符號使用的字元。 預設值是 | (直立線符號或分隔號)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<int >  
 指定 Analysis Services 引擎在結束追蹤之前等候的秒數 (如果您指定 -TraceFile 參數的話)。 如果在指定的時間週期內沒有記錄追蹤訊息，追蹤會被視為已完成。 預設的追蹤逾時值是 5 秒。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|5|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-tracelevel-traceleveloption"></a>-TraceLevel \<TraceLevelOption >  
 指定追蹤檔中要收集和記錄的資料。 可能的值包括 High、Medium、Low、Duration、DurationResult。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|高|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|PSObject|  
|輸出|字串|  
  
## <a name="example-1-xmla-input-file"></a>範例 1 (XMLA 輸入檔)  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 這個命令會執行 XMLA 指令碼，以便傳回伺服器上的使用中連接清單。 DiscoverConnections.xmla 檔案包含下列 XMLA 指令碼：  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>範例 2 (TMSL 輸入檔)  
 此範例與第一個範例完全相同，但指定碼是 TMSL (JSON) 並需要 SQL Server 2016 的表格式執行個體。 您可以在 SQL Server Management Studio 中產生 TMSL 指令碼。  
  
 如果有多個執行個體，而且您的表格式執行個體是具名執行個體，請記得設定伺服器名稱︰  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>範例 3 (查詢)  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 探索 XMLA 查詢會傳回 Analysis Server 可用的資料來源和連接這些資料來源的必要資訊。 結果是 XML 格式。 若要改善可讀性，您可以透過管道將輸出傳送至 XML 檔案 (例如，將 `| Out-file C:\Results\XMLAQueryOutput.xml` 附加至命令)，然後在支援結構化 XML 的瀏覽器或其他應用程式中檢視結果。  
  
  
  
