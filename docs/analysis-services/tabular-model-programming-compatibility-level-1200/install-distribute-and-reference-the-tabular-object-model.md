---
title: "安裝、 散佈及參考表格式物件模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e51769f7-aac7-4835-a5ae-91aac04aa476
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9688a692d25d484b05bca88e0779d2812944f3af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>安裝、 散佈及參考表格式物件模型

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

本文說明如何下載、 參考以及轉散發 Analysis Services 表格式物件模型 (TOM)，來建立及管理表格式模型與資料庫中的 managed 程式碼的 C# 程式庫。  
  
TOM 是隨附於 SQL Server 2016 AMO 用戶端程式庫 (Microsoft.AnalysisServices.dll) 擴充功能。 它可搭配 SQL Server 2016 版本中的表格式中繼資料引擎為目標的表格式模型。 若要使用 TOM，必須是模型與資料庫相容性層級 1200年或更高。  

## <a name="amo-tom-assemblies"></a>AMO TOM 組件

SQL Server 2016 重構，並擴大要包含新的核心、 表格式和 JSON 組件的 AMO。 它也會包含原始的 AMO 組件，Microsoft.AnalysisServices.dll 自第一次發行以來已分析服務的一部分。 Restructured 的 AMO 卸載至一個組件，通用類別，並提供表格式和多維度 Api 之間以邏輯方式透過其他組件。 

下表描述每個組件。
  
組件  |功能  |重要類別 |
---------|---------|--------------  |
核心 <br/>Microsoft.AnalysisServices.Core.dll | 常見的表格式和多維度資料庫。 <br/><br/>提供例外狀況處理、 泛型連接到 Analysis Services 執行個體和資料庫，以及存取通用屬性和伺服器和資料庫物件的方法。 <br/><br/>目標 SQL Server 2016 任何 AMO 解決方案所需。 | 核心&nbsp;伺服器<br/>核心&nbsp;資料庫<br/>AmoException
TOM<br/> Microsoft.AnalysisServices.Tabular.dll、 13.0.1601.5 版本或更新版本。| 建立及管理表格式中繼資料物件。 | TOM&nbsp;伺服器 <br/>TOM&nbsp;資料庫<br /> 模型<br /> Table<br /> 資料行<br /> 關聯性
  AMO<br /> Microsoft.AnalysisServices.dll| 建立和管理多維度中繼資料物件，包括表格式 1050年-1103年資料庫。 | AMO&nbsp;伺服器 <br />AMO&nbsp;資料庫 <br /> Cube <br /> 維度 <br /> MeasureGroup 
Json<br/>Microsoft.AnalysisServices.Tabular.Json.dll | 協助程式 DLL 包裝 NewtonSoftJson.dll (JSON.NET) 來控制更新 Analysis Services 工作負載中的 JSON 序列化中引進的功能變更的風險。 <br /> <br />這個 DLL 為 TOM 的相依性存在，而且不打算直接用於程式碼。 | 無。  
  
 ### <a name="understanding-assembly-dependencies"></a>了解組件相依性
  
若要針對 AMO 程式，您的方案必須包含相依 Dll 的參考。 AMO 和 TOM 取決於核心因為它提供基底類別。

因為 AMO 中的某些類別參考類別從 TOM，AMO 會取決於 TOM。 例如，AMO 資料庫物件有一個屬性的型別模型中，TOM dll 中實作模型。 

![AMO TOM 相依性](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

您無法發佈 Microsoft.AnalysisServices.dll 沒有 Microsoft.AnalysisServices.Tabular.dll，但您可以參考其各自的命名空間，而沒有其他。

### <a name="choosing-which-namespace-to-use-in-code"></a>選擇要在程式碼中使用哪一個命名空間

在[物件階層](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)，資料庫 下的任何物件都是透過模型物件的表格式中繼資料建構或經由 Cube、 維度或量值群組物件的多維度中繼資料建構。 在伺服器、 資料庫、 角色或追蹤層級的高層級作業，的選擇来參考的命名空間將取決於工作負載您的程式碼必須支援。

* 使用 Tabular.Server 或 Tabular.Database，如果您的方案是相容性層級 1200年或更高，而且您使用的資料庫物件必須提供給模型、 資料表、 資料行，以及表示表格式中繼資料建構為其他物件的存取。
* 使用 AnalysisServices.Server 或 AnalysisServices.Database 如果下游程式碼參考多維度物件，例如 Cube、 資料來源、 DataSourceViews 和維度。

您將需要兩個命名空間的工具和應用程式支援的資料庫和模型類型的混合。 

參考程式碼中的核心命名空間是不必要的。核心中的類別是為了提供通用屬性，例如名稱和描述，主要物件建立的基底類別。  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>判斷是否需要 AMO 和 TOM 安裝  
   
 AMO 和 TOM 會集結成套單一用戶端程式庫中。 如果您已安裝的 SQL Server 2016 Analysis Services 執行個體、 用戶端程式庫或為目標的 SQL Server 2016年執行個體的 SQL Server Data Tools 的版本，Microsoft.AnalysisServices.dll 已安裝。  
  
 若要判斷是否已安裝的組件，請檢查這些位置：
* C:\Windows\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13。MSSQLSERVER\OLAP\bin
 
 確認下列組件存在：
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>下載 SQL_AS_AMO  
 
 請注意，Microsoft.AnalysisServices.dll 不會透過 NuGet 管理員可用。
  
1. 移至[的 SQL Server 2016 功能套件下載頁面](https://www.microsoft.com/download/details.aspx?id=52676)。  
  
2. 按一下 [下載]。  
  
3. 選取  **\X64\SQL_AS_AMO.msi**或**\X86\SQL_AS_AMO.msi**。 您可以選擇其中一個： AMO 和 TOM 組件是平台限制。
  
4. 按一下**下一步**以便進行下載。 您會發現.msi 檔案中的您**下載**資料夾。  
  
## <a name="install-sqlasamo"></a>安裝 SQL_AS_AMO  
  
1. 按兩下**SQL_AS_AMO.msi**並逐步執行安裝。  
  
2. 移至**C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies**確認 Microsoft.AnalysisServices.Core.dll、 Microsoft.AnalysisServices.dll、 Microsoft.AnalysisServices.Tabular.dll，放置和Microsoft.AnalysisServices.Tabular.Json.dll。   
  
## <a name="add-references"></a>加入參考  
  
1. 在**方案總管 中** > **將參考加入** > **瀏覽**。  
2. 移至**C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies**選取：  
   * Microsoft.AnalysisServices.Core  
   * Microsoft.AnalysisServices.Tabular  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. 按一下 **[確定]**。  在**方案總管 中**，確認組件都在 參考 資料夾。
  
4. 在您的程式碼 頁面上，加入 Microsoft.AnalysisServces.Tabular 命名空間，即使資料庫和模型為表格式 1200年或更高的相容性層級。 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    （選擇性） 加入 Microsoft.AnalysisServces 支援廣泛的不是特別是 SQL Server 2016 表格式伺服器模式的 Analysis services 執行個體的連接。 
 
    當包含有通用類別伺服器、 資料庫、 角色和追蹤物件的命名空間，避免模稜兩可的參考來限定要使用哪一個命名的空間 （例如，Microsoft.AnalysisServices.Tabular.Server 具現化伺服器使用物件的表格式命名空間）。

## <a name="redistribute-amo-and-tom-with-your-application"></a>隨您的應用程式轉散發 AMO 和 TOM  
  
轉散發的 AMO 和 TOM 是透過**sql_as_amo.msi**安裝套件。 如果您要建立安裝程式在用戶端應用程式呼叫到 AMO 或 TOM，新增**sql_as_amo.msi**您可執行檔。 這是轉散發的 AMO 和 TOM 用戶端程式庫的唯一支援的機制。  
  
套件是獨立的並提供所有組件所需的程式碼中呼叫 AMO 和 TOM。 其他封裝，例如 SQL_AS_OLEDB.msi 或 SQL_AS_ADOMD.msi，並不特別需要 TOM 程式設計案例。

