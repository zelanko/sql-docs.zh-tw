---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: 描述 SQL Server Management Studio 環境之元件和基本設定選項的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 51fb197c3b5177c699134a48fc4888cd134e1711
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>教學課程：SQL Server Management Studio 元件和設定
本教學課程介紹 SQL Server Management Studio (SSMS) 中不同視窗元件以及工作區中的一些基本設定選項。 在本文中，您將學習關於： 

> [!div class="checklist"]
> * 組成 SSMS 環境的不同元件
> * 變更環境配置並將其重設為預設值
> * 將查詢編輯器最大化
> * 變更字型 
> * 設定啟動選項 
> * 將設定重設回預設值 

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio。  

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 元件
本節涵蓋工作區中可用的不同視窗元件及其用途。 

- 可透過在標題列的角落點擊 X 來關閉每個視窗元件，然後從主功能表中的 [檢視] 下拉式清單重新開啟。 

    ![檢視功能表](media/ssms-configuration/viewmenu.png)

- **物件總管** (F8)：物件總管是含有伺服器中所有資料庫物件的樹狀檢視。 這可以包括 SQL Server Database Engine、Analysis Services、Reporting Services 和 Integration Services 的資料庫。 物件總管含有它所連接的所有伺服器的資訊。 
    
    ![物件總管](media/ssms-configuration/objectexplorer.png)
- **查詢視窗** (Ctrl + N)：按一下 [新增查詢] 後，您將在此視窗中鍵入 Transact-SQL (T-SQL) 查詢。 您的查詢結果也會顯示在這裡。
    
    ![新增查詢視窗](media/ssms-configuration/newquery.png)

- **屬性** (F4)：在開啟 [查詢視窗] 後即可見，並會顯示查詢的基本屬性。 例如，會顯示查詢開始的時間、傳回的資料列數目和連線詳細資料。  

    ![屬性](media/ssms-configuration/properties.png)

- **範本瀏覽器** (Ctrl + Alt + T)：在範本瀏覽器中可以找到許多預先建立的 T-SQL 範本。 這些範本可讓您執行各種功能，例如建立或備份資料庫。 

    ![範本瀏覽器](media/ssms-configuration/templates.png)

- **物件總管詳細資料** (F7)：這是物件總管中可見內容的更細微檢視，並可讓您一次管理多個物件。 例如，物件總管詳細資料視窗可讓您同時選取多個資料庫，並將其刪除或撰寫指令碼。 

    ![物件總管詳細資料](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>變更環境配置 
本節討論如何管理環境配置，如移動各種視窗。 

-  透過按住標題並拖曳視窗，可以移動每個視窗元件。 
- 透過在標題列中選取圖釘圖示，可以釘選和取消釘選每個視窗元件：
    
    ![釘選物件](media/ssms-configuration/pushpin.png)

- 每個視窗元件都有一個下拉式箭頭，允許以各種方式操作視窗： 

    ![視窗選項](media/ssms-configuration/windowoptions.png)

- 一旦您有兩個或更多個查詢視窗開啟時，可以垂直或水平將其索引標籤，以使兩個查詢視窗立即可見。 若要實現這一點，請以滑鼠右鍵按一下查詢標題，並選取所需的索引標籤選項。 
 
    ![查詢索引標籤選項](media/ssms-configuration/querytabbedoptions.png)

    - 這是**水平索引標籤群組**：![水平索引標籤群組](media/ssms-configuration/horizontaltab.png)     
    
    - 這是**垂直索引標籤群組**：  
        ![垂直索引標籤群組](media/ssms-configuration/verticaltabgroup.png)
        

    - 若要再次合併索引標籤，請以滑鼠右鍵按一下查詢標題，並 [移至下一個索引標籤群組] 或 [移至上一個索引標籤群組]：
    
        ![合併查詢索引標籤](media/ssms-configuration/mergetabgroups.png)

- 若要還原預設環境配置，請按一下 [視窗] 功能表 > [重設視窗配置]：
 
    ![還原視窗配置](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>將查詢編輯器最大化
查詢編輯器可以最大化為全螢幕模式。

1. 按一下查詢編輯器視窗中的任何位置。
2. 按 SHIFT + ALT + ENTER 鍵來切換全螢幕模式和一般模式。 

這個鍵盤快速鍵適用於任何文件視窗。 



## <a name="change-basic-settings"></a>變更基本設定
本節討論如何修改 SSMS 中的一些基本設定。 這些選項可在 [工具] 功能表選項中找到：

  ![工具功能表](media/ssms-configuration/tools.png)


- 醒目標示的工具列可以透過功能表進行修改：[工具] > [自訂]：

    ![自訂工具列](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>變更字型
- 字型可從功能表進行變更：[工具] > [選項] > [字型和色彩]：

     ![字型和色彩](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>變更啟動選項
- 啟動選項會決定您首次啟動 SSMS 時的工作區外觀。 這些可以從功能表設定：[工具] > [選項] > [啟動]：
 
    ![啟動選項](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>將設定重設為預設
- 所有這些設定可以從功能表匯出和匯入：[工具] > [匯入和匯出設定] 

    ![匯入和匯出設定](media/ssms-configuration/settings.png)
    - 這也是您可以將所有設定重設為預設的地方。 


## <a name="next-steps"></a>後續步驟
下一篇文章會告訴您使用 SSMS 時的幾個額外秘訣和訣竅，例如尋找您的 SQL Server 錯誤記錄檔和 SQL 執行個體名稱。 

請前往下一篇文章來進一步了解
> [!div class="nextstepaction"]
> [按鈕](ssms-tricks.md)
 
 




