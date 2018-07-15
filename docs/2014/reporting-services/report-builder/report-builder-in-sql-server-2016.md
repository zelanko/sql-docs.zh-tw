---
title: SQL Server 2014 報表產生器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
caps.latest.revision: 29
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 911b88bc7b707e837bbd042814a2f8e84a61daa0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261924"
---
# <a name="report-builder-in-sql-server-2014"></a>SQL Server 2014 中的報表產生器
  報表產生器是一種報表撰寫環境的商務使用者想要工作[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Office 環境。 當您設計報表時，可以指定要取得資料的位置、要取得的資料，以及要顯示資料的方式。 當您執行報表時，報表處理器會採用已指定的所有資訊、擷取資料，然後將它與報表配置結合，以便產生報表。 您可以在報表產生器中預覽報表，也可以將報表發行至報表伺服器或處於 SharePoint 整合模式的報表伺服器，讓其他人執行報表。  
  
 下圖中的報表提供一個矩陣，內含資料列和資料行群組、走勢圖、指標以及位於邊角資料格的摘要圓形圖，並附有一份地圖，地圖中具有兩組以色彩和圓形大小呈現的地理資料。  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="JumpStartReptCreation"></a> 開始建立報表  
  
-   **啟動報表 withreport 組件**小組的其他人建立的。 報表組件是已個別發行至報表伺服器或與報表伺服器整合之 SharePoint 網站上的報表項目。 報表組件可以在其他報表中重複使用。 諸如資料表、矩陣、圖表和影像等報表項目都可以發行為報表組件。  
  
-   **共用資料集開始**小組的其他人建立的。 共用資料集是以儲存到報表伺服器或與報表伺服器整合之 SharePoint 網站上之共用資料來源做為基礎的查詢。  
  
-   **從資料表、矩陣或圖表精靈開始**。 您可以選擇資料來源連接、拖放欄位以建立資料集查詢、選取配置和樣式，以及自訂報表。  
  
-   **從地圖精靈開始** ，以建立根據地理或幾何背景顯示彙總資料的報表。 地圖資料可能是來自 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或環境系統研究協會 (Environmental Systems Research Institute, Inc.) 的空間資料。(ESRI) 形狀檔。 您也可以新增[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Bing 地圖底圖背景。  
  

  
##  <a name="DesignRept"></a> 設計報表  
  
-   **建立含有資料表、 矩陣、 圖表和自由形式報表配置報表。** 針對以資料行為基礎的資料建立資料表報表、針對摘要資料建立矩陣報表 (例如交叉分析或樞紐分析表報表)、針對地理資料建立圖表報表，以及針對其他資料建立自由形式的報表。 報表可以內嵌其他報表和圖表，連同動態網路架構應用程式的清單、圖形和控制項。  
  
-   **從各種資料來源建立報表。** 使用具有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]管理的資料提供者、OLE DB 提供者或 ODBC 資料來源之任何資料來源類型中的資料建立報表。 您可以建立使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、Oracle、Hyperion 及其他資料庫中關聯式和多維度資料的報表。 您可以使用 XML 資料處理延伸模組，從任何 XML 資料來源擷取資料。 您可以使用資料表值函數來設計自訂資料來源。  
  
-   **修改現有的報表。** 使用報表產生器，您可以自訂及更新報表中所建立的[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]報表設計工具。  
  
-   **修改您的資料**透過篩選、 分組和排序資料，或是加入公式和運算式。  
  
-   **加入圖表、量測計、走勢圖和指標** ，以視覺化格式摘要列出資料，並且一次展示大量的彙總資訊。  
  
-   **加入互動式功能** ，例如文件引導模式、顯示/隱藏按鈕，以及子報表和鑽研報表的鑽研連結。 您可以使用參數和篩選來篩選自訂檢視表的資料。  
  
-   **內嵌或參考影像與其他資源** ，包括外部內容。  
  

  
##  <a name="ManageRpt"></a> 管理報表  
  
-   **將報表定義儲存** 至電腦或報表伺服器，以便管理報表以及與其他人共用報表。  
  
-   在開啟報表時或開啟報表後，**選擇呈現格式** 。 您可以選取 Web 導向、頁面導向，以及桌面應用程式的格式。 格式包括 HTML、MHTML、PDF、XML、CSV、TIFF、Word 及 Excel。  
  
-   **設定訂閱。** 當您將報表發行至報表伺服器或處於 SharePoint 整合模式的報表伺服器之後，就可以將報表設定成在特定時間執行、建立報表記錄，以及設定電子郵件訂閱。  
  
-   使用 Reporting Services Atom 轉譯延伸模組，從報表**產生資料摘要** 。  
  
> [!NOTE]  
>  報表伺服器管理員會在報表伺服器或處於 SharePoint 整合模式的報表伺服器上管理已發行的報表。 報表伺服器管理員可以定義安全性、設定屬性以及排程作業，例如報表記錄和電子郵件報表傳遞。 他們可以建立共用排程和共用資料來源，讓它們可供一般使用。 管理員也會管理所有報表伺服器資料夾。 執行管理工作的能力需視使用者權限而定。  
  

  
##  <a name="InThisSection"></a> 本節內容  
 [SQL Server 2014 報表產生器的新功能](../what-s-new-in-report-builder-for-sql-server-2014.md)  
 描述此版本報表產生器的新功能，包括地圖。  
  
 [教學課程： 建立快速圖表報表離線](tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 介紹報表產生器以及可協助您建立報表的精靈。 此教學課程會提供一組資料供您使用，所以您不需要連接至資料來源以便開始作業。  
  
 [規劃報表&#40;報表產生器&#41;](../report-design/planning-a-report-report-builder.md)  
 提供有關開始建立報表之前應該考量之事項的資訊。  
  
 [報表撰寫概念&#40;報表產生器及 SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 定義整個報表產生器文件集中使用的重要概念。  
  
 [報表設計檢視&#40;報表產生器&#41;](report-design-view-report-builder.md)  
 說明報表設計檢視的不同窗格和區域。  
  
 [共用資料集設計檢視&#40;報表產生器&#41;](shared-dataset-design-view-report-builder.md)  
 說明共用資料集設計檢視的不同窗格和區域。  
  
 [鍵盤快速鍵&#40;報表產生器&#41;](keyboard-shortcuts-report-builder.md)  
 概述報表產生器中可用於導覽及設計報表的快速鍵。  
  
 [啟動報表產生器&#40;報表產生器&#41;](start-report-builder.md)  
 說明如何啟動兩種不同版本的報表產生器：單機版和 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版。  
  
  
