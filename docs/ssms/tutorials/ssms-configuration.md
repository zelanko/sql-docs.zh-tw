---
title: 教學課程：SQL Server Management Studio 元件和設定
description: 描述 SQL Server Management Studio 環境之元件和基本設定選項的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: jroth
ms.openlocfilehash: a7ad0d94985871e422146a531b3084127d58e7e7
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834519"
---
# <a name="sql-server-management-studio-components-and-configuration"></a>SQL Server Management Studio 元件和設定

本教學課程介紹 SQL Server Management Studio (SSMS) 中的各種視窗元件，以及工作區中的一些基本設定選項。 在此文章中，您將學會如何： 

> [!div class="checklist"]
> * 識別組成 SSMS 環境的元件
> * 變更環境配置，並將它重設為預設值
> * 將查詢編輯器最大化
> * 變更字型
> * 設定啟動選項
> * 將設定重設為預設值

## <a name="prerequisites"></a>Prerequisites

若要完成本教學課程，您需要 SQL Server Management Studio。  

* 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 元件

本節描述工作區中可用的各種視窗元件，以及如何使用它們。

* 若要關閉視窗，請選取標題列右上角的 **X**。
* 若要重新開啟視窗，請選取 [檢視]  功能表中的視窗。

    ![[檢視] 功能表](media/ssms-configuration/viewmenu.png)

* **物件總管** (F8)：物件總管是含有伺服器中所有資料庫物件的樹狀檢視。 該檢視包含 SQL Server 資料庫引擎、SQL Server Analysis Services、SQL Server Reporting Services 和 SQL Server Integration Services 的資料庫。 [物件總管] 含有它所連線之所有伺服器的資訊。 

    ![物件總管](media/ssms-configuration/objectexplorer.png)
* **查詢視窗** (Ctrl+N)：選取 [新增查詢]  之後，在這個視窗中輸入 Transact-SQL (T-SQL) 查詢。 此處也會顯示您的查詢結果。

    ![新增查詢視窗](media/ssms-configuration/newquery.png)

* **屬性** (F4)：查詢視窗開啟時，您會看到 [屬性] 檢視。 該檢視會顯示查詢的基本屬性。 例如，會顯示查詢開始的時間、傳回的資料列數目和連線詳細資料。  

    ![屬性](media/ssms-configuration/properties.png)

* **範本瀏覽器** (Ctrl+Alt+T)：[範本瀏覽器] 具有各種預先建立的 T-SQL 範本。 您可以使用這些範本來執行各種功能，例如建立或備份資料庫。 

    ![範本瀏覽器](media/ssms-configuration/templates.png)

* **物件總管詳細資料** (F7)：此檢視會比使用 [物件總管] 中的檢視更精細。 您可以使用 [物件總管詳細資料]，同時管理多個物件。 例如，在這個視窗中，您可以選取多個資料庫，然後同時加以刪除或編寫其指令碼。 

    ![物件總管詳細資料](media/ssms-configuration/objectexplorerdetails.PNG) 

## <a name="change-the-environment-layout"></a>變更環境配置 

本節描述如何變更環境配置，例如如何移動各種視窗。 

* 若要移動視窗，請按住標題，然後拖曳視窗。 
* 若要釘選或取消釘選視窗，請選取標題列中的圖釘圖示：

    ![釘選物件](media/ssms-configuration/pushpin.png)

* 每個視窗元件都具有您可以用各種方式操作視窗的下拉式功能表： 

    ![視窗選項](media/ssms-configuration/windowoptions.png)

* 當您有兩個或更多個開啟的查詢視窗時，可以垂直或水平使視窗成為索引標籤，讓兩個查詢視窗均為可見。 若要檢視索引標籤式視窗，請在查詢的標題上按一下滑鼠右鍵，然後選取您想要的索引標籤式選項：

    ![查詢索引標籤選項](media/ssms-configuration/querytabbedoptions.png)

    * 以下是水平索引標籤群組：

      ![水平索引標籤群組的範例](media/ssms-configuration/horizontaltab.png)

    * 以下是垂直索引標籤群組：

      ![垂直索引標籤群組的範例](media/ssms-configuration/verticaltabgroup.png)

    * 若要合併索引標籤，請以滑鼠右鍵按一下查詢標題，然後選取 [移至上一個索引標籤群組]  或 [移至下一個索引標籤群組]  ：

      ![合併查詢索引標籤](media/ssms-configuration/mergetabgroups.png)

* 若要還原預設環境配置，請在 [視窗]  功能表中選取 [重設視窗配置]  ：

    ![還原視窗配置](media/ssms-configuration/resetwindowlayout.png)

## <a name="maximize-query-editor"></a>將查詢編輯器最大化

您可以將查詢編輯器最大化為全螢幕模式：

1. 按一下 [查詢編輯器] 視窗中的任何位置。

2. 按 Shift+Alt+Enter 鍵來切換全螢幕模式和一般模式。 

這個鍵盤快速鍵適用於任何文件視窗。 

## <a name="change-basic-settings"></a>變更基本設定

本節描述如何從 [工具]  功能表中修改 SSMS 的某些基本設定。

  ![工具功能表](media/ssms-configuration/tools.png)

* 若要修改反白顯示的工具列，請選取 [工具]   > [自訂]  ：

    ![自訂工具列](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>變更字型

* 若要變更字型，請選取 [工具]   > [選項]   > [字型和色彩]  ：

     ![變更字型和色彩](media/ssms-configuration/fontsandcolors.png)

### <a name="change-startup-options"></a>變更啟動選項

* 啟動選項會決定您首次開啟 SSMS 時的工作區外觀。 若要變更啟動選項，請選取 [工具]   > [選項]   > [啟動]  ：

    ![變更啟動選項](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-the-default"></a>將設定重設為預設值

* 您可以從功能表中匯出並匯入所有的這些設定。 若要匯入或匯出設定，或還原預設設定，請選取 [工具]   > [匯入和匯出設定]  

    ![匯入和匯出設定](media/ssms-configuration/settings.png)

## <a name="next-steps"></a>後續步驟

熟悉 SSMS 的最佳方式是實際練習。 這些「教學課程」  與「操作方式」  文章可協助您使用 SSMS 內所提供的各種功能。  這些文章會告訴您如何管理 SSMS 的元件及如何尋找您經常使用的功能。

* [連線至執行個體並對其進行查詢](connect-query-sql-server.md)
* [指令碼](scripting-ssms.md)
* [在 SSMS 中使用範本](../template/templates-ssms.md)
* [使用 SSMS 的其他提示與訣竅](ssms-tricks.md)