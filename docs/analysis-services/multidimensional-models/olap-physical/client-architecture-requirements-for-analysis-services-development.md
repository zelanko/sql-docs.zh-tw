---
title: 用戶端架構需求，針對 Analysis Services 開發 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef45e149fc70fdf338a60cd823497eb2efb6a215
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022385"
---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Analysis Services 開發的用戶端架構需求
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援精簡型用戶端架構。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]計算引擎是完全伺服器為基礎，因此所有的查詢會在伺服器上解析。 所以，每一個查詢只需要用戶端和伺服器之間單次往返，使得查詢越來越複雜時可擴充效能。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的原生通訊協定是 XML for Analysis (XML/A)。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 為用戶端應用程式提供數個資料存取介面，但所有這些元件均使用 XML for Analysis 與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體進行通訊。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 提供數個不同的提供者，來支援不同的程式設計語言。 提供者與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器的通訊方式，是透過 Internet Information Services (IIS)，經由 TCP/IP 或 HTTP 來傳送和接收 SOAP 封包中的 XML for Analysis。 HTTP 連接使用 IIS 具現化的 COM 物件，叫作資料幫浦，做為 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料的導管。 資料幫浦絕不會檢查 HTTP 資料流所包含的基礎資料，任何基礎資料結構也不可以供資料程式庫本身的任何程式碼使用。  
  
 ![Analysis Services 的邏輯用戶端架構](../../../analysis-services/multidimensional-models/olap-physical/media/as-clientarch9.gif "Analysis Services 的邏輯用戶端架構")  
  
 Win32 用戶端應用程式可使用 OLE DB for OLAP 介面，或元件物件模型 (COM) 自動化語言的 Microsoft® ActiveX® Data Objects (ADO) 物件模型，例如 Microsoft Visual Basic®，來連接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 以 .NET 語言撰寫的應用程式可使用 ADOMD.NET 連接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。  
  
 現有的應用程式可以在不修改的情況下，使用其中一個 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 提供者來與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 進行通訊。  
  
|程式設計語言|資料存取介面|  
|--------------------------|---------------------------|  
|C++|OLE DB for OLAP|  
|Visual Basic 6|ADO MD|  
|.NET 語言|ADO MD.NET|  
|任何支援 SOAP 的語言|XML for Analysis|  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 含有一個 Web 架構，具有可供小型和大型組織部署的完全可擴充中介層。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 為 Web 服務提供廣泛的中介層支援。 OLE db for OLAP 和 ADO MD 支援 ASP 應用程式，ADOMD.NET 支援 ASP.NET 應用程式。 下圖所說明的中間層可擴充至許多並行使用者。  
  
 ![中介層架構的邏輯圖表](../../../analysis-services/multidimensional-models/olap-physical/media/as-midtierarch9.gif "中間層架構的邏輯圖表")  
  
 用戶端和中介層應用程式兩者都可以直接與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 進行通訊，而毋需使用提供者。 用戶端和中介層應用程式可經由 TCP/IP、HTTP 或 HTTPS，在 SOAP 封包中傳送 XML for Analysis。 可使用任何支援 SOAP 的語言，撰寫用戶端程式碼。 此案例中的通訊由 Internet Information Services (IIS) 使用 HTTP 來管理最簡單，不過，也需要撰寫程式碼來使用 TCP/IP 直接連接到伺服器。 這是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的最精簡型用戶端方案。  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>表格式或 SharePoint 模式下的 Analysis Services  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，xVelocity 記憶體中分析引擎 (VertiPaq) 模式的表格式資料庫中，可以啟動伺服器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]已經發行至 SharePoint 網站的活頁簿。  
  
 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 是建立及查詢分別使用 SharePoint 或表格式模式之記憶體中資料庫唯一支援的用戶端環境。 內嵌[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]您使用 Excel 建立的資料庫和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]工具包含在 Excel 活頁簿，並當做 Excel.xlsx 檔案的一部分儲存。  
  
 不過，如果您將儲存在傳統 Cube 的資料匯入 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿中，活頁簿就可以使用此資料。 如果另一個 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿已發行至 SharePoint 網站，您也可以從該活頁簿匯入資料。  
  
> [!NOTE]  
>  當您使用 Cube 做為 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿的資料來源時，從 Cube 取得的資料是定義為 MDX 查詢；不過資料是以扁平化快照集方式匯入。 您無法以互動方式使用資料或從 Cube 重新整理資料。  
  
 如需有關使用 SSAS cube 做為資料來源的詳細資訊，請參閱[適用於 Excel 的 Power Pivot](http://go.microsoft.com/fwlink/?LinkId=164234)。  
  
### <a name="interfaces-for-power-pivot-client"></a>Power Pivot 用戶端的介面  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 透過建立的介面和語言的 Analysis Services xVelocity 記憶體中分析引擎 (VertiPaq) 儲存引擎，在活頁簿內與互動： AMO 和 ADOMD.NET，以及 MDX 和 XMLA。 在增益集內，透過類似 Excel 的公式語言，即資料分析運算式 (DAX)，來定義量值。 DAX 運算式內嵌於傳送至同處理序伺服器的 XMLA 訊息。  
  
### <a name="providers"></a>提供者  
 之間的通訊[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和 Excel 會使用 MSOLAP OLEDB 提供者 （11.0 版）。 在 MSOLAP 提供者內，有四個不同的模組 (或傳輸) 可用於用戶端和伺服器之間傳送訊息。  
  
 **TCP/IP**用於一般的用戶端伺服器連接。  
  
 **HTTP**用於透過 SSAS 資料幫浦服務或由 SharePoint 呼叫的 HTTP 連接[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]Web 服務 (WS) 元件。  
  
 **INPROC**用於連線至同處理序引擎。  
  
 **通道**保留供溝通[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]SharePoint 伺服陣列中的系統服務。  
  
## <a name="see-also"></a>另請參閱  
 [OLAP 引擎伺服器元件](../../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md)  
  
  
