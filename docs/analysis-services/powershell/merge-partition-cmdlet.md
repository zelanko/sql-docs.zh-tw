---
title: "Merge-Partition 指令程式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 15c7b069-897d-4bc8-a808-59cbeeabe4d8
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Merge-Partition 指令程式
  將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。  
  
## 語法  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## 說明  
 Merge-Partition 指令程式會將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。 只能合併符合下列所有準則的資料分割：  
  
-   資料分割位於相同的量值群組中。  
  
-   資料分割位於相同的電腦上。  
  
-   資料分割共用相同的儲存模式 (多維度資料庫的 MOLAP、HOLAP 和 ROLAP)。  
  
## 參數  
  
### -Name \<字串>  
 指定要合併來源資料分割資料的目標資料分割。 此資料分割必須已存在。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -SourcePartition \<字串>  
 指定要合併至目標資料分割的來源資料分割。 您可以建立要合併之資料分割的逗號分隔清單。 使用變數來儲存清單。 例如，$Sources=”Sales_2008”, “Sales_2009”, “Sales_2010”。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Database \<字串>  
 指定資料分割所屬的資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Cube \<字串>  
 指定資料分割所屬的 Cube。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -MeasureGroup \<字串>  
 指定資料分割所屬的量值群組。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Server \<字串>  
 指定指令程式將會連接並執行的 Analysis Services 執行個體。 如果沒有提供伺服器名稱，則會建立 localhost 的連接。 若為預設執行個體，請單獨指定伺服器名稱。 若為具名執行個體，請使用格式 servername\instancename。 若為 HTTP 連接，請使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|localhost|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Credential \<PSCredential>  
 若為您已經設定為 HTTP 存取的執行個體，這個參數是在使用 Analysis Service 執行個體的 HTTP 連接時用來傳入使用者名稱和密碼。 如需詳細資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)和 [Analysis Services 中的 PowerShell 指令碼](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)來進行 HTTP 連接。  
  
 如果指定了此參數，使用者名稱和密碼將會用來連接到指定的 Analysis Server 執行個體。 如果沒有指定認證，則會使用執行此工具之使用者的預設 Windows 帳戶。  
  
 若要使用此參數，請先使用 Get-Credential 來建立 PSCredential 物件，以便指定使用者名稱和密碼 (例如 `$Cred=Get-Credential “adventure-works\bobh”`。 然後，您可以透過管道將這個物件傳送至 -Credential 參數 `(-Credential:$Cred`)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|True (ByValue)|  
|接受萬用字元？|false|  
  
### -TargetPartition \<Microsoft.AnalysisServices.Partition>  
 指定要合併來源資料分割的目標資料分割。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### \<CommonParameters>  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|System.string|  
|輸出|無|  
  
## 範例 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 這個命令將 2001、2002 和 2003 的資料分割合併至 2004 的資料分割中，然後刪除之前年度的資料分割。  
  
## 請參閱＜  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [使用 PowerShell 管理表格式模型](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  