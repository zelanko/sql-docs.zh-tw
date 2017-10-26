---
title: "判斷變更資料是否就緒 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],determining readiness
ms.assetid: 04935f35-96cc-4d70-a250-0fd326f8daff
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 91c0f342c63df8d3a1376850615c5b68745ab4c9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="determine-whether-the-change-data-is-ready"></a>判斷變更資料是否就緒
  在執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的控制流程中，第二個工作是確保所選間隔之變更資料已就緒。 由於非同步的擷取程序可能還沒有處理到所選端點的所有變更，因此這是必要的步驟。  
  
> [!NOTE]  
>  控制流程的第一個工作是計算變更間隔的端點。 如需這項工作的詳細資訊，請參閱[指定變更資料的間隔](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md)。 如需設計控制流程之完整程序的描述，請參閱[變更資料擷取 &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="understanding-the-components-of-the-solution"></a>了解方案的元件  
 本主題所描述的方案使用 4 個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件：  
  
-   重複評估「執行 SQL」工作之輸出的「For 迴圈」容器。  
  
-   可查詢異動資料擷取程序維護然後使用此資訊判斷資料是否就緒之特殊資料表的「執行 SQL」工作。  
  
-   實作資料未就緒時處理之延遲的元件。 這可以是「指令碼」工作或「執行 SQL」工作。  
  
-   (選擇性) 當「執行 SQL」工作傳回表示錯誤或逾時狀況的值時，報告錯誤或逾時的元件。  
  
 這些元件會設定或讀取數個封裝變數的值以控制在迴圈內部或稍後在封裝中執行的流程。  
  
#### <a name="to-set-up-package-variables"></a>設定封裝變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 **[變數]** 視窗中，建立下列變數：  
  
    1.  建立具有整數資料類型的變數，以保存「執行 SQL」工作傳回的狀態值。  
  
         此範例會使用變數名稱 DataReady，其初始值為 0。  
  
    2.  建立變數以便在資料尚未就緒時，保存要延遲的期間。 如果您要使用「指令碼」工作實作延遲，變數的資料類型應為整數。 如果您要搭配 WAITFOR 陳述式使用「執行 SQL」工作，變數的資料類型應該為字串，才能接受諸如 "00:00:10" 的值。  
  
         此範例會使用變數名稱 DelaySeconds，其初始值為 10。  
  
    3.  建立具有整數資料類型的變數，以保存迴圈的目前反覆運算。  
  
         此範例會使用變數名稱 TimeoutCount，其初始值為 0。  
  
    4.  建立具有整數資料類型的變數，以指定報告逾時狀況前，迴圈應該測試資料的次數。  
  
         此範例會使用變數名稱 TimeoutCeiling，其初始值為 20。  
  
    5.  (選擇性) 建立具有整數資料類型的變數，用於表示變更資料的第一個載入。  
  
         此範例會使用變數名稱 IntervalID，並僅針對 0 這個值進行檢查以表示初始載入。  
  
## <a name="configuring-a-for-loop-container"></a>設定 For 迴圈容器  
 在設定變數的情況下，「For 迴圈」容器是第一個要加入的元件。  
  
#### <a name="to-configure-a-for-loop-container-to-wait-until-change-data-is-ready"></a>設定 For 迴圈容器以便等到變更資料就緒  
  
1.  在 **設計師的** [控制流程] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 索引標籤上，將「For 迴圈」容器加入到控制流程中。  
  
2.  將計算間隔端點的「執行 SQL」工作連接到「For 迴圈」容器。  
  
3.  在 **[For 迴圈編輯器]**中，選取下列選項：  
  
    1.  針對 **InitExpression**，輸入 `@DataReady = 0`。  
  
         此運算式會設定迴圈變數的初始值。  
  
    2.  針對 **EvalExpression**m，輸入 `@DataReady == 0`。  
  
         當此運算式評估為 **False**時，執行會通過迴圈之外，而且會開始累加式載入。  
  
## <a name="configuring-the-execute-sql-task-that-queries-for-change-data"></a>設定查詢變更資料的執行 SQL 工作  
 在「For 迴圈」容器的內部，您可以加入「執行 SQL」工作。 此工作會查詢異動資料擷取程序在資料庫中維護的資料表。 此查詢的結果是一個狀態值，表示變更資料是否就緒。  
  
 在下表中，第一欄顯示範例 Transact-SQL 查詢從「執行 SQL」工作傳回的值。 第二欄顯示其他元件如何回應這些值。  
  
|傳回值|意義|回應|  
|------------------|-------------|--------------|  
|0|表示變更資料尚未就緒。<br /><br /> 沒有晚於所選間隔之結束點的異動資料擷取記錄。|執行會繼續進行實作延遲的元件。 然後，控制會傳回「For 迴圈」容器，只要傳回的值為 0，就會繼續檢查「執行 SQL」工作。|  
|1|可能表示尚未擷取完整間隔的變更資料，或該變更資料已遭刪除。 這會被視為錯誤狀況。<br /><br /> 沒有早於所選間隔之起始點的異動資料擷取記錄。|執行會繼續進行記錄錯誤的選擇性元件。|  
|2|表示資料已就緒。<br /><br /> 沒有早於所選間隔之起始點，也沒有晚於所選間隔之結束點的異動資料擷取記錄。|執行會通過「For 迴圈」容器之外，而且會開始累加式載入。|  
|3|表示所有可用變更資料的初始載入。<br /><br /> 條件式邏輯會從僅用於此用途的特殊封裝變數取得這個值。|執行會通過「For 迴圈」容器之外，而且會開始累加式載入。|  
|5|表示已達到 TimeoutCeiling。<br /><br /> 資料的迴圈已經測試過指定的次數，而且資料仍然無法使用。 如果沒有這個測試或類似的測試，封裝可能會無期限地執行。|執行會繼續進行記錄逾時的選擇性元件。|  
  
#### <a name="to-configure-an-execute-sql-task-to-query-whether-change-data-is-ready"></a>設定執行 SQL 工作查詢變更資料是否就緒  
  
1.  在「For 迴圈」容器的內部，加入「執行 SQL」工作。  
  
2.  在 **[執行 SQL 工作編輯器]**的 **[一般]** 頁面上，選取下列選項：  
  
    1.  針對 **[ResultSet]**，選取 **[單一資料列]**。  
  
    2.  將有效的連接設定到來源資料庫。  
  
    3.  針對 **[SQLSourceType]**，選取 **[直接輸入]**。  
  
    4.  針對 **[SQLStatement]**，輸入下列 SQL 陳述式：  
  
        ```  
        declare @DataReady int, @TimeoutCount int  
  
        if not exists (select tran_end_time from cdc.lsn_time_mapping  
                where tran_end_time > ?  )  
            select @DataReady = 0  
        else  
            if ? = 0  
                select @DataReady = 3   
        else  
            if not exists (select tran_end_time from cdc.lsn_time_mapping  
                    where tran_end_time <= ? )  
                select @DataReady = 1   
        else  
            select @DataReady = 2  
  
        select @TimeoutCount = ?  
        if (@DataReady = 0)  
            select @TimeoutCount = @TimeoutCount + 1  
        else  
            select @TimeoutCount = 0  
  
        if (@TimeoutCount > ?)  
            select @DataReady = 5  
  
        select @DataReady as DataReady, @TimeoutCount as TimeoutCount  
  
        ```  
  
3.  在 **[執行 SQL 工作編輯器]** 的 **[參數對應]**頁面上，進行下列對應：  
  
    1.  將 ExtractEndTime 變數對應到參數 0。  
  
    2.  將 IntervalID 變數對應到參數 1。  
  
    3.  將 ExtractStartTime 變數對應到參數 2。  
  
    4.  將 TimeoutCount 變數對應到參數 3。  
  
    5.  將 TimeoutCeiling 變數對應到參數 4。  
  
4.  在 **[執行 SQL 工作編輯器]** 的 **[結果集]**頁面上，將 DataReady 結果對應到 DataReady 變數，並將 TimeoutCount 結果對應到 TimeoutCount 變數。  
  
## <a name="waiting-until-the-change-data-is-ready"></a>等到變更資料就緒  
 變更資料尚未就緒時，您可以使用數個方法中的一個方法來實作延遲。 下列兩個程序說明如何使用「指令碼」工作或「執行 SQL」工作實作延遲。  
  
> [!NOTE]  
>  先行編譯的指令碼所產生的負擔比「執行 SQL」工作所產生的負擔少。  
  
#### <a name="to-implement-a-delay-by-using-a-script-task"></a>使用指令碼工作實作延遲  
  
1.  在「For 迴圈」容器的內部，加入「指令碼」工作。  
  
2.  將查詢以判斷變更資料是否就緒的「執行 SQL」工作連接到新的「指令碼」工作。  
  
3.  針對將「執行 SQL」工作連接到「指令碼」工作的優先順序條件約束，開啟 **[優先順序條件約束編輯器]** ，然後選取下列選項：  
  
    1.  針對 **[評估作業]**，選取 **[運算式與條件約束]**。  
  
    2.  針對 **[數值]**，選取 **[成功]**。  
  
         **[成功]** 的條件約束值會參考前一個工作的成功。 在這個情況下是「執行 SQL」工作的成功。  
  
    3.  針對 **[運算式]**，輸入 `@DataReady == 0 && @TimeoutCount <= @TimeoutCeiling`。  
  
    4.  選取 **[邏輯 AND。所有的條件約束都必須評估為 True]** (如果尚未選取)。  
  
4.  在 **[指令碼工作編輯器]**的 **[指令碼]** 頁面上，針對 **[ReadOnlyVariables]**，選取清單中的 **[User::DelaySeconds]** 整數變數。  
  
5.  在 **[指令碼工作編輯器]**的 **[指令碼]** 頁面上，按一下 **[編輯指令碼]** 來開啟指令碼開發環境。  
  
6.  在 Main 程序中，輸入下列其中一個程式碼行：  
  
    -   如果您是以 C# 撰寫程式，輸入下列程式碼行：  
  
        ```  
        System.Threading.Thread.Sleep((int)Dts.Variables["DelaySeconds"].Value * 1000);  
        ```  
  
         \- 或 -  
  
    -   如果您是以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]撰寫程式，輸入下列程式碼行：  
  
        ```  
        System.Threading.Thread.Sleep(Ctype(Dts.Variables("DelaySeconds").Value, Integer) * 1000)  
  
        ```  
  
        > [!NOTE]  
        >  **Thread.Sleep** 方法應為以毫秒指定的引數。  
  
7.  保留從指令碼之執行傳回 **DtsExecResult.Success** 的預設程式碼行。  
  
8.  關閉指令碼開發環境以及 **[指令碼工作編輯器]**。  
  
#### <a name="to-implement-a-delay-by-using-an-execute-sql-task"></a>使用執行 SQL 工作實作延遲  
  
1.  在「For 迴圈」容器的內部，加入「執行 SQL」工作。  
  
2.  將查詢以判斷變更資料是否就緒的「執行 SQL」工作連接到新的「執行 SQL」工作。  
  
3.  針對連接兩個「執行 SQL」工作的優先順序條件約束，開啟 **[優先順序條件約束編輯器]** ，然後選取下列選項：  
  
    1.  針對 **[評估作業]**，選取 **[運算式與條件約束]**。  
  
    2.  針對 **[數值]**，選取 **[成功]**。  
  
         **[成功]** 的條件約束值會參考前一個「執行 SQL」工作的成功。  
  
    3.  針對 **[運算式]**，輸入 `@DataReady == 0`。  
  
    4.  選取 **[邏輯 AND。所有的條件約束都必須評估為 True]** (如果尚未選取)。  
  
         此選項需要條件約束和運算式兩個條件必須同時為 true。  
  
4.  在 **[執行 SQL 工作編輯器]**的 **[一般]** 頁面上，選取下列選項：  
  
    1.  針對 **[ResultSet]**，選取 **[單一資料列]**。  
  
    2.  將有效的連接設定到來源資料庫。  
  
    3.  針對 **[SQLSourceType]**，選取 **[直接輸入]**。  
  
    4.  針對 **[SQLStatement]**，輸入下列 SQL 陳述式：  
  
        ```  
        WAITFOR DELAY ?  
  
        ```  
  
5.  在編輯器的 **[參數對應]** 頁面上，將 DelaySeconds 字串變數對應到參數 0。  
  
## <a name="handling-an-error-condition"></a>處理錯誤條件  
 您可以在迴圈內部，選擇性地設定其他元件，以記錄錯誤或逾時條件：  
  
-   此元件可以在 DataReady 變數的值 = 1 時，記錄錯誤條件。 這個值表示在所選間隔開始前，沒有可用的變更資料。  
  
-   此元件也可以在達到 Timeout Ceiling 變數的值時，記錄逾時條件。 這個值表示資料的迴圈已經測試過指定的次數，而且資料仍然無法使用。 如果沒有這個測試或類似的測試，封裝可能會無期限地執行。  
  
#### <a name="to-configure-an-optional-script-task-to-log-an-error-condition"></a>設定選擇性的指令碼工作以記錄錯誤條件  
  
1.  如果您要將訊息寫入記錄檔藉以報告錯誤或逾時，請設定封裝的記錄。 如需詳細資訊，請參閱 [在 SQL Server Data Tools 中啟用封裝記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#ssdt)。  
  
2.  在「For 迴圈」容器的內部，加入「指令碼」工作。  
  
3.  將查詢以判斷變更資料是否就緒的「執行 SQL」工作連接到新的「指令碼」工作。  
  
4.  針對將「執行 SQL」工作連接到「指令碼」工作的優先順序條件約束，開啟 **[優先順序條件約束編輯器]** ，然後選取下列選項：  
  
    1.  針對 **[評估作業]**，選取 **[運算式與條件約束]**。  
  
    2.  針對 **[數值]**，選取 **[成功]**。  
  
         **[成功]** 的條件約束值會參考前一個工作的成功。 在這個情況下是「執行 SQL」工作的成功。  
  
    3.  針對 **[運算式]**，輸入 `@DataReady == 1 || @DataReady == 5`。  
  
    4.  選取 **[邏輯 AND。所有的條件約束都必須評估為 True]** (如果尚未選取)。  
  
         此選項需要條件約束和運算式兩個條件必須同時為 true。  
  
5.  在 **[指令碼工作編輯器]**的 **[指令碼]** 頁面上，針對 **[ReadOnlyVariables]**，從清單選取 **[User::DataReady]** 和 **[User::ExtractStartTime]** ，讓其值可以用於指令碼中。  
  
     如果您要將來自特定系統變數 (例如，System::PackageName) 的資訊加入到您要寫入記錄檔的資訊，請同時選取這些變數。  
  
6.  在 **[指令碼工作編輯器]**的 **[指令碼]** 頁面上，按一下 **[編輯指令碼]** 來開啟指令碼開發環境。  
  
7.  在 Main 程序中，呼叫 **Dts.Log** 方法來輸入程式碼以記錄錯誤，或呼叫 **Dts.Events** 介面的其中一個方法來引發事件。 傳回 `Dts.TaskResult = Dts.Results.Failure`以通知封裝發生錯誤。  
  
     下列範例顯示如何將訊息寫入到記錄檔中。 如需相關資訊，請參閱 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)、 [Raising Events in the Script Task](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)及 [Returning Results from the Script Task](../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)。  
  
    ```  
    ' User variables.  
    Dim dataReady As Integer = _  
      CType(Dts.Variables("DataReady").Value, Integer)  
    Dim extractStartTime As Date = _  
      CType(Dts.Variables("ExtractStartTime").Value, DateTime)  
  
    ' System variables.  
    Dim packageName As String = _  
      Dts.Variables("PackageName").Value.ToString()  
    Dim executionStartTime As Date = _  
      CType(Dts.Variables("StartTime").Value, DateTime)  
  
    Dim eventMessage As New System.Text.StringBuilder()  
  
    If dataReady = 1 OrElse dataReady = 5 Then  
  
      If dataReady = 1 Then  
        eventMessage.AppendLine("Start Time Error")  
      Else  
        eventMessage.AppendLine("Timeout Error")  
      End If  
  
      With eventMessage  
        .Append("The package ")  
        .Append(packageName)  
        .Append(" started at ")  
        .Append(executionStartTime.ToString())  
        .Append(" and ended at ")  
        .AppendLine(DateTime.Now().ToString())  
        If dataReady = 1 Then  
          .Append("The specified ExtractStartTime was ")  
          .AppendLine(extractStartTime.ToString())  
        End If  
      End With  
  
      System.Windows.Forms.MessageBox.Show(eventMessage.ToString())  
  
      Dts.Log(eventMessage.ToString(), 0, Nothing)  
  
      Dts.TaskResult = Dts.Results.Failure  
  
    Else  
  
      Dts.TaskResult = Dts.Results.Success  
  
    End If  
  
    ```  
  
8.  關閉指令碼開發環境以及 **[指令碼工作編輯器]**。  
  
## <a name="next-step"></a>下一個步驟  
 判斷變更資料就緒後，下一個步驟是準備針對變更資料進行查詢。  
  
 **下一個主題：**[準備查詢變更資料](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)  
  
  

