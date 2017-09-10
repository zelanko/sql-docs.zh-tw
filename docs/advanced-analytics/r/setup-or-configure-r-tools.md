---
title: "安裝或設定 R 工具 | Microsoft Docs"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>安裝或設定 R 工具
  Microsoft R Server 提供開發與測試 R 程式碼所需的所有基底 R 程式庫、一組 ScaleR 套件，以及標準 R 工具。 不過，如果想要使用專用的 R 開發環境，有數種可用的開發環境，包括許多免費工具。  
  
## <a name="basic-r-tools"></a>基本 R 工具  
 Microsoft R Server 安裝中不需要其他工具，因為預設會安裝 R「基底安裝」中包含的所有標準 R 工具。

-   **RTerm**：用來執行 R 指令碼的命令列工具 
  
-   **RGui.exe**：R 的簡單互動式編輯器。RGui.exe 和 RTerm 的命令列引數相同。 
  
-   **RScript**：以批次模式執行 R 指令碼的命令列工具。  

若要找出這些工具，請尋找 R 程式庫的位置。 R 程式庫的位置取決於您是否僅安裝 SQL Server R Services，或者您也安裝了 R Server (獨立式)。 如需詳細資訊，請參閱[安裝的項目以及尋找 R 套件位置](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1)

然後，查看資料夾 `..\R_SERVER\bin\x64`。  

> [!TIP]  
>  需要 R 工具的說明嗎？ 文件會包含於安裝資料夾 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 中，以及 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual` 中。  
>   
>  或者，只需開啟 [RGui]，按一下 [說明]，然後選取其中一個選項。  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R Client 可供免費下載，讓您能夠開發 R 方案，以便在 Microsoft R Server 或者 SQL Server R Services 中輕鬆地執行。 此選項針對可能無法存取 R Server (只在企業版中提供) 的資料科學家，協助其開發使用 ScaleR 的方案。 

如果您以不同的 R 開發環境 (例如 Visual Studio R 工具或 RStudio) 來使用 ScaleR，您必須指定 Microsoft R Client 做為 R 可執行檔來使用。 雖然效能會受到限制，但這樣可提供您 RevoScaleR 套件和 Microsoft R Server 其他功能的完整存取權。

您也可以使用 R Client 中提供的工具 (例如 RGui 和 RTerm) 來執行指令碼，或撰寫並執行特定 R 程式碼。

[安裝 Microsoft R Client (英文)](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="bkmk_RTools"></a> Visual Studio R 工具  

 為了方便使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，請考慮使用 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 做為您的開發環境。 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 是 Visual Studio 的一個免費增益集，適用於所有版本的 Visual Studio。 Visual Studio 也支援 Python 和 F# 整合。  

 如需安裝指示，請參閱[如何安裝 R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。

> [!TIP]
> 在您安裝新的套件之前，請檢查預設使用的 R 執行階段。 否則，很可能會將新的 R 套件安裝到預設程式庫位置，而無法從 R Server 找出它們！


## <a name="rstudio"></a>RStudio

如果您偏好使用 RStudio，需要一些額外步驟才能使用 RevoScaleR 程式庫︰
- 安裝 Microsoft R Server 或 Microsoft R Client，以取得必要的套件和程式庫。
- 更新您的 R 路徑，以使用 R Server 執行階段。

如需詳細資訊，請參閱[設定您的 IDE (英文)](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)。


## <a name="see-also"></a>另請參閱  
 [建立獨立式 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [開始使用 Microsoft R Server &#40;獨立&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

