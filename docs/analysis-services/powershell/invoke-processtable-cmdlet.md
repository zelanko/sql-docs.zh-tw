---
title: "Invoke-processtable cmdlet |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e2a7f1392931ec5edd41803f6df6d98aa95403dd
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="invoke-processtable-cmdlet"></a>Invoke-ProcessTable Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在具有特定 **RefreshType** 的 **Table** 上進行 **Process**作業。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## <a name="parameters"></a>參數  
  
### <a name="-tablename-string"></a>-TableName \<string>  
 資料分割隸屬的必要處理資料表名稱。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<string>  
 指定資料表所屬的資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Server\<Microsoft.AnalysisSevices.Server>  
 選擇性地指定如果您不是使用 **SQLAS** 提供者目錄作為內容時要連接的伺服器執行個體。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType>  
 指定表格式資料庫的處理類型。  有效值為 Full、ClearValues、Calculate、DataOnly、Automatic、Add 和 Defragment。 如需說明與指引，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-credential"></a>-Credential  
 如果指定了此參數，傳遞的使用者名稱和密碼將會用來連接到 Analysis Services 執行個體。 如果沒有指定認證，則會假設為執行指令碼之使用者的預設 Windows 帳戶。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-whatif"></a>-Whatif  
 包含此參數，以在執行之前取得作業影響的資訊。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-confirm"></a>-Confirm  
 包含此參數，以在作業執行之前以是或否回應的互動方式來確認作業。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？||  
|預設值||  
|接受管線輸入？||  
|接受萬用字元？|false|  
  
## <a name="example-1"></a>範例 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 此命令會使用管道傳送要處理之資料表的識別。  
  
## <a name="example-2"></a>範例 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 此命令會使用 **enum** 重新整理類型處理表格式中繼資料資料表。  
  
  
