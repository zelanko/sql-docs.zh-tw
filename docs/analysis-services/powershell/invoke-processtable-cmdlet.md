---
title: "Invoke-ProcessTable Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessTable Cmdlet
  在具有特定 **RefreshType** 的 **Table** 上進行 **Process** 作業。  
  
 此 Cmdlet 只適用於 SQL Server 2016 相容性層級 1200 的表格式模型。  
  
## 語法  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## 參數  
  
### -TableName \<字串>  
 資料分割隸屬的必要處理資料表名稱。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -DatabaseName \<字串>  
 指定資料表所屬的資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Server\<Microsoft.AnalysisSevices.Server>  
 選擇性地指定如果您不是使用 **SQLAS** 提供者目錄作為內容時要連接的伺服器執行個體。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -RefreshType \<Microsoft.AnalysisServices.RefreshType>  
 指定相容性層級 1200 的表格式資料庫的處理類型。  有效值為 Full、ClearValues、Calculate、DataOnly、Automatic、Add 和 Defragment。 如需說明與指引，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Credential  
 如果指定了此參數，傳遞的使用者名稱和密碼將會用來連接到 Analysis Services 執行個體。 如果沒有指定認證，則會假設為執行指令碼之使用者的預設 Windows 帳戶。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Whatif  
 包含此參數，以在執行之前取得作業影響的資訊。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Confirm  
 包含此參數，以在作業執行之前以是或否回應的互動方式來確認作業。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？||  
|預設值||  
|接受管線輸入？||  
|接受萬用字元？|false|  
  
## 範例 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 此命令會使用管道傳送要處理之資料表的識別。  
  
## 範例 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 此命令會使用 **enum** 重新整理類型處理表格式中繼資料資料表。  
  
## 請參閱＜  
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  