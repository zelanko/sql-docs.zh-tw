---
title: 進階檢視 SQL Server 中擴充事件的目標資料 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ea4a9169218f517aa186e1913bd952c4665a48e
ms.sourcegitcommit: 209fa6dafe324f606c60dda3bb8df93bcf7af167
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66198321"
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>進階檢視 SQL Server 中擴充事件的目標資料

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


本文說明如何使用 SQL Server Management Studio (SSMS.exe) 的進階功能來檢視豐富詳細資料中擴充事件的目標資料。 本文說明如何︰


- 使用各種方式來開啟和檢視目標資料。
- 針對擴充事件使用特殊功能表或工具列，以將目標資料匯出為各種格式。
- 在檢視時或在匯出之前操作資料。



### <a name="prerequisites"></a>Prerequisites

現有的文章假設您已經知道如何建立和啟動事件工作階段。 下文提早示範如何建立事件工作階段的指示︰

[快速入門：SQL Server 中的擴充事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


本文也假設您已安裝最新每月發行的 SSMS。 安裝說明位於：

- [下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)



### <a name="differences-with-azure-sql-database"></a>Azure SQL Database 差異


在 Microsoft SQL Server 和 Azure SQL Database 這兩項產品中，擴充事件的實作和功能會有較高程度的同位檢查。 但有一些差異會影響 SSMS UI (使用者介面)。


- 針對 SQL Database，package0.event_file 目標不能是本機磁碟機上的檔案。 相反地，您必須使用 Azure 儲存體容器。 因此，當您連接到 SQL Database 時，SSMS UI 會要求儲存體容器，而不是本機路徑和檔案名稱。


- 在 SSMS UI 中，看到 [監看即時資料]  核取方塊呈現灰色並停用時，原因是該功能不適用於 SQL Database。


- 一些擴充事件會與 SQL Server 一起安裝。 在 [工作階段]  節點下，可以看到 [AlwaysOn_health]  加上一些其他項目。 因為 SQL Database 沒有這些項目，所以連接至 SQL Database 時看不到這些項目。


從 SQL Server 的角度寫入現有的文章。 本文使用 event_file 目標，這是其中一個差異區域。 進一步提及任何差異限於重要或不明顯的差異。


如需 Azure SQL Database 特有擴充事件的文件，請參閱︰

- [Azure SQL Database 中的擴充事件](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. 一般選項


通常，您可以透過下列方式存取進階選項︰


- [檔案]   > [開啟]   > [檔案]  的一般功能表。
- 以滑鼠右鍵按一下物件總管  的 [管理]   > [擴充事件]  。
- 特殊功能表 [擴充事件]  ，以及擴充事件的特殊工具列。
- 以滑鼠右鍵按一下可顯示目標資料的索引標籤式窗格。



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. 將目標資料帶入 SSMS 以供顯示


有各種方法可將 event_file 目標資料帶入 SSMS UI。 當您指定 event_file 目標時，可以設定其檔案路徑和名稱︰

- .XEL 是檔案名稱的副檔名。


- 每次啟動事件工作階段時，系統會將大整數內嵌至新的檔案名稱，讓檔案名稱設為唯一，而且與啟動工作階段的上述情況不同。
  - *範例：* Checkpoint_Begins_ES_0_131103935140400000.xel


- .XEL 內的內容不是可使用 Notepad.exe 檢視的純文字。
  - 如果要的話，同時附加數個 .XEL 檔案的方式是使用功能表 [檔案]   > [開啟]   > [合併擴充的事件檔案]  。



SSMS 可以顯示任何目標的資料。 但是，各種目標的顯示畫面會不同︰

- *event_file：* 會充分顯示 event_file 目標的資料，並提供豐富的功能。


- *ring_buffer：* 通道緩衝區目標的資料顯示會為原始 XML。


- 對於其他目標，顯示的功能是介於 event_file 與 ring_buffer 之間。
  - 這類其他目標包括 event_counter、histogram 和 pair_matching。


- *etw_classic_sync_target：* SSMS 無法顯示目標類型 etw_classic_sync_target 的資料。



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 使用功能表 [檔案] > [開啟] > [檔案] 開啟 .XEL


您可以使用標準功能表 [檔案]   > [開啟]   > [檔案]  開啟個別 .XEL 檔案。

您也可以將 .XEL 檔案拖放至 SSMS UI 中的索引標籤列。



### <a name="b2-view-target-data"></a>B.2 檢視目標資料


[檢視目標資料]  選項會顯示目前為止已擷取的資料。


在物件總管  窗格中，您可以展開節點，再以滑鼠右鍵按一下︰

- [管理]   > [擴充事件]   > [工作階段]   >  *[your-session]*  >  *[your-target-node]*  > [檢視目標資料]  。


目標資料會顯示在 SSMS 的索引標籤式窗格中。 這會顯示在下列螢幕擷取畫面中。


![您的目標 > 檢視目標資料](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> [檢視目標資料]  顯示指定事件工作階段的「多個 .XEL 檔案的累積資料」  。 每個「啟動  -停止」  循環會建立名稱中內嵌稍後時間衍生整數的檔案，但每個檔案都共用相同的根名稱。



#### <a name="b3-watch-live-data"></a>B.3 監看即時資料


如果事件工作階段目前使用中，您可能想要在目標接收事件資料時即時監看事件資料。


- [管理]   > [擴充事件]   > [工作階段]   >  *[your-session]*  > [監看即時資料]  。


![您的工作階段 > 監看即時資料](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


會以指定的間隔更新資料顯示。 請查看下列位置中的 [分派延遲上限]  ：

- [擴充事件]   > [工作階段]   >  *[your-session]*  > [屬性]   > [進階]   > [分派延遲上限] 



### <a name="b4-view-xel-with-sysfnxefiletargetreadfile-function"></a>B.4 使用 sys.fn_xe_file_target_read_file 函數檢視 .XEL


對於批次處理，下列系統函數可以產生 .XEL 檔案中記錄的 XML：

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. 匯出目標資料


SSMS 中有目標資料之後，即可執行下列動作以將資料匯出為各種格式︰


1. 將焦點放在資料顯示。
    - 擴充事件的新工具列和新功能表項目會突然變成可見。

    ![匯出顯示的資料，擴充事件 > 匯出至 > (.csv、.xel 或資料表)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. 按一下新的功能表項目 [擴充事件]  。
3. 按一下 [匯出至]  ，然後選擇格式。



## <a name="d-manipulate-data-in-the-display"></a>D. 操作顯示中的資料


SSMS UI 提供數種方式來操作資料，但只是檢視資料。



### <a name="d1-context-menus-in-the-data-display"></a>D.1 資料顯示中的操作功能表


以滑鼠右鍵按一下時，資料顯示中的不同位置會提供不同的操作功能表。



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 以滑鼠右鍵按一下資料格


下列螢幕擷取畫面顯示以滑鼠右鍵按一下資料顯示中的資料格時出現的操作功能表。 此螢幕擷取畫面也會顯示 [複製]  功能表項目的展開。


![以滑鼠右鍵按一下資料顯示中的資料格](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 以滑鼠右鍵按一下資料行標頭


下列螢幕擷取畫面顯示以滑鼠右鍵按一下 [時間戳記]  標頭時出現的操作功能表。


![以滑鼠右鍵按一下資料顯示中的資料行標頭， 以及詳細資料方格。](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


上述螢幕擷取畫面也會顯示擴充事件的特殊工具列。 [詳細資料] 按鈕的亮度指出按鈕使用中。 因此，影像也會顯示 [詳細資料]  索引標籤，而且方格會呈現為資料顯示的第二個部分。



### <a name="d2-choose-columns-merge-columns"></a>D.2 選擇資料行，合併資料行


[選擇資料行]  選項可讓您控制要顯示和不要顯示的資料行。 您可以在一些不同的位置中找到 [選擇資料行]  功能表項目︰

- 在 [擴充事件]  功能表上。
- 在擴充事件工具列上。
- 在資料顯示中標頭的操作功能表上。


按一下 [選擇資料行]  時，會顯示同名的對話方塊。


![[選擇資料行] 對話方塊，也提供 [合併資料行] 選項](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 合併資料行


[選擇資料行]  對話方塊包含一個區段，基於下列目的而專供將多個資料行合併成一個資料行：

- 顯示。
- 匯出。



### <a name="d3-filters"></a>D.3 篩選


在擴充事件的區域中，您可以指定兩種主要類型的篩選︰

- *預先目標篩選：* 可讓事件引擎傳送至目標的資料量減少的篩選。

- *後置目標篩選：* 您可以在 SSMS UI 中選取以排除部分目標記錄而不顯示的篩選。


SSMS 顯示篩選如下︰

- 「時間範圍」  篩選，可檢查 [時間戳記]  資料行。
- 「資料行值」  篩選。


時間篩選與資料行篩選之間的關聯性是布林值 '*AND*'。


![[篩選] 對話方塊上的時間範圍和資料行篩選](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 群組和彙總


透過比對指定資料行中的值以將資料列群組在一起，是資料摘要彙總的首要步驟。



#### <a name="d41-grouping"></a>D.4.1 群組


在擴充事件工具列上，[群組]  按鈕會啟動對話方塊，以用來將指定資料行的顯示資料群組在一起。 下一個螢幕擷取畫面顯示一個對話方塊，用來依 *name* 資料行進行群組。

![[工具列] > [群組] 按鈕，然後是 [群組] 對話方塊](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

群組達成之後，顯示會有新的外觀，如下所示。

![群組後的新顯示外觀](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 彙總


群組顯示的資料之後，即可繼續彙總其他資料行中的資料。  下一個螢幕擷取畫面顯示群組資料是透過 *count*進行彙總。

![[工具列] > [彙總] 按鈕，然後是 [彙總] 對話方塊](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

彙總達成之後，顯示會有新的外觀，如下所示。

![[工具列] > [彙總] 按鈕，然後是 [彙總] 對話方塊](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 檢視執行階段查詢計劃


**query_post_execution_showplan** 事件可讓您在 SSMS UI 中查看實際查詢計劃。 顯示 [詳細資料]  窗格時，您可以在 [查詢計劃]  索引標籤上看到查詢計劃圖形。將滑鼠游標停留在查詢計劃的節點上方，即可看到節點之屬性名稱和其值的清單。


![查詢計劃，具有一個節點的屬性清單](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)

## <a name="see-also"></a>另請參閱

[XELite：跨平台程式庫，用來讀取 XEL 檔案或即時 SQL 串流中的 XEvent](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/)，於 2019 年 5 月發行。
