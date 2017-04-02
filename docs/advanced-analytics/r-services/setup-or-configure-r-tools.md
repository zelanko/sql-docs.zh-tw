---
title: "設定或設定 R 工具 | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 設定或設定 R 工具
  Microsoft R Server 提供所有基底的 R 程式庫、 小數位數的 R 封裝和標準 R 工具，您需要開發和測試 R 程式碼。 不過，如果您想要使用專用的 R 開發環境，有數個可用，包括許多可用工具。  
  
## <a name="basic-r-tools"></a>基本的 R 工具  
 其他工具中不需要安裝 Microsoft R 伺服器，因為所有標準的 R 工具包含在 *基底安裝* 的 R 預設會安裝。

-   **RTerm**︰ 執行 R 指令碼的命令列工具 
  
-   **RGui.exe**: R 的簡單互動式編輯器命令列引數是 RGui.exe 和 RTerm 相同。 
  
-   **RScript**︰ 批次模式下的命令列工具執行 R 指令碼。  

根據預設，這些工具會安裝在下列資料夾︰
- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- SQL Server vNext: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  需要其他協助嗎？ R 工具文件位於安裝資料夾︰ `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 和 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`。  
>   
>  或者，只需開啟 **RGui**, ，按一下 [ **協助**, ，然後選取其中一個選項。  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R 用戶端是免費下載，可讓您開發 R 解決方案，可在 Microsoft R server 或 SQL Server R Services 中輕鬆地執行。

通常您會安裝不同的 R 開發環境，例如 Visual Studio 或 RStudio，R 工具，然後指定 [Microsoft R 用戶端當做 R 可執行檔。 這可讓您完整存取權 RevoScaleR 封裝和其他 Microsoft R Server 功能。

您也可以使用熟悉的工具，例如 RGui 和 RTerm 來執行指令碼或撰寫和執行臨機操作的 R 程式碼。

[安裝 Microsoft R 用戶端](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> R Tools for Visual Studio  

 為了方便使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，請考慮使用 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 做為開發環境。 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 適用於所有版本的 Visual Studio 的 Visual studio 是免費的增益集。 Visual Studio 也提供 Python 和 F # 的整合支援。  

如需詳細資訊，請參閱 [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/)。

 本節說明如何安裝 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 使用免費的社群版本的 Visual Studio。  
  
#### <a name="install-visual-studio"></a>安裝 Visual Studio  
  
1.  免費的 Visual Studio Community edition 是可以從這個頁面下載︰ [Visual Studio Community](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  下載完成後，按一下 [ **執行** ，然後選取要安裝的元件。  
  
     如果您執行自訂安裝程式，請注意 Microsoft Web 開發人員元件所需。  
  
3.  選擇 **一般** 目前設定。 當您安裝 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], ，您必須將變更為針對 R 開發自訂的版面配置 toption。  

#### <a name="add-the-r-tools"></a>新增 R 工具

Visual Studio 安裝之後，延伸模組可供 R、 Python 和許多其他語言透過 **選項** 功能表。

4. 從功能表列中，按一下 [工具]，然後選取 **擴充功能和更新**。

5. 安裝的一端，R 工具會偵測到可用的電腦上，並詢問您是否要變更您的開發環境，Microsoft R 伺服器或 R 執行階段使用 R 執行階段，Microsoft R 用戶端的 R 執行階段版本。

如果安裝程式偵測不到您想要使用的 R 伺服器執行階段，您可以變更它以手動方式隨時使用 **選項** 功能表。 如需詳細資訊，請參閱 [設定您的 IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)。

## <a name="rstudio"></a>RStudio

如果您想要使用 RStudio，採取下列額外的步驟，以使用 RevoScaleR 程式庫︰
- 安裝 Microsoft R Server 或 Microsoft R Client 來取得必要的套件和程式庫。
- 更新您的 R 路徑，以便使用適當的 R 執行階段。

如需詳細資訊，請參閱 [設定您的 IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)。


## <a name="see-also"></a>另請參閱  
 [建立獨立 R 伺服器](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [開始使用 Microsoft R Server & #40。獨立 &#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  