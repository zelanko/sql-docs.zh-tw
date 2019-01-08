---
title: 準備查詢變更資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 831e44cb232dea7f0730c73d360cd787f3895878
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756990"
---
# <a name="prepare-to-query-for-the-change-data"></a>準備查詢變更資料
  在執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的控制流程中，第三個工作 (也就是最後一個工作) 是準備查詢變更資料，並加入「資料流程」工作。  
  
> [!NOTE]  
>  控制流程的第二個工作是確保所選間隔的變更資料已就緒。 如需這項工作的詳細資訊，請參閱[判斷變更資料是否就緒](determine-whether-the-change-data-is-ready.md)。 如需設計控制流程之完整程序的描述，請參閱[異動資料擷取 &#40;SSIS&#41;](change-data-capture-ssis.md)。  
  
## <a name="design-considerations"></a>設計考量  
 若要擷取異動資料，您將呼叫 Transact-SQL 資料表值函式，接受間隔的端點做為輸入參數，並傳回指定之間隔的異動資料。 資料流程中的來源元件會呼叫這個函數。 如需此來源元件的資訊，請參閱 [擷取與了解變更資料](retrieve-and-understand-the-change-data.md)。  
  
 最常用的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源元件 (包括 OLE DB 來源、ADO 來源和 ADO NET 來源) 無法衍生資料表值函式的參數資訊。 因此，多數來源無法直接呼叫參數化函數。  
  
 您有兩個設計選項，可傳遞函數的輸入參數：  
  
-   **將參數化的查詢組合成字串**。 您可以使用「指令碼」工作或「執行 SQL」工作，利用硬式編碼到字串的參數值，組合動態 SQL 字串。 然後，您可以將此字串儲存在封裝變數中，並將其用於設定來源元件的 SqlCommand 屬性。 由於來源元件不再需要參數資訊，因此這個方式會成功。  
  
    > [!NOTE]  
    >  先行編譯的指令碼所產生的負擔比「執行 SQL」工作所產生的負擔少。  
  
-   **使用參數化的包裝函式**。 或者，您可以建立參數化的預存程序，當做呼叫參數化資料表值函式的包裝函數。 由於來源元件可以成功衍生預存程序的參數資訊，因此這個方式會成功。  
  
 本主題使用第一個設計選項，並將參數化的查詢組合成字串。  
  
## <a name="preparing-the-query"></a>準備查詢  
 在您可以將輸入參數的值串連到單一查詢字串前，您必須設定查詢所需的封裝變數。  
  
#### <a name="to-set-up-package-variables"></a>設定封裝變數  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [變數] 視窗中，建立具有字串資料類型的變數，以保存「執行 SQL」工作所傳回的查詢字串。  
  
     這個範例會使用變數名稱 SqlDataQuery。  
  
 建立封裝變數後，您可以使用「指令碼」工作或「執行 SQL」工作來串連輸入參數的值。 下列兩個程序描述如何設定這些元件。  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>使用指令碼工作串連查詢字串  
  
1.  在 [控制流程] 索引標籤上，將「指令碼」工作加入「For 迴圈」容器後的封裝中，然後將「For 迴圈」容器連接到該工作。  
  
    > [!NOTE]  
    >  此程序假設封裝會從單一資料表執行累加式載入。 如果封裝從多個資料表載入，而且擁有包含多個子封裝的父封裝，則會將此工作當做第一個元件，加入到每個子封裝中。 如需詳細資訊，請參閱 [執行多個資料表的累加式載入](perform-an-incremental-load-of-multiple-tables.md)。  
  
2.  在 [指令碼工作編輯器] 的 [指令碼] 頁面上，選取下列選項：  
  
    1.  針對 [ReadOnlyVariables]，選取 [User::DataReady]、[User::ExtractStartTime] 和 [User::ExtractEndTime]。  
  
    2.  針對 [ReadWriteVariables]，從清單中選取 [User::SqlDataQuery]。  
  
3.  在 **[指令碼工作編輯器]** 的 **[指令碼]** 頁面上，按一下 **[編輯指令碼]** 來開啟指令碼開發環境。  
  
4.  在 Main 程序中，輸入下列其中一個程式碼區段：  
  
    -   如果您是以 C# 撰寫程式，輸入下列程式碼行：  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \-或-  
  
    -   如果您是以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]撰寫程式，輸入下列程式碼行：  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  保留從指令碼之執行傳回 `DtsExecResult.Success` 的預設程式碼行。  
  
6.  關閉指令碼開發環境以及 **[指令碼工作編輯器]**。  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>使用執行 SQL 工作串連查詢字串  
  
1.  在 [控制流程] 索引標籤上，將「執行 SQL」工作加入「For 迴圈」容器後的封裝中，然後將「For 迴圈」容器連接到此工作。  
  
    > [!NOTE]  
    >  此程序假設封裝會從單一資料表執行累加式載入。 如果封裝從多個資料表載入，而且擁有包含多個子封裝的父封裝，則會將此工作當做第一個元件，加入到每個子封裝中。 如需詳細資訊，請參閱 [執行多個資料表的累加式載入](perform-an-incremental-load-of-multiple-tables.md)。  
  
2.  在 **[執行 SQL 工作編輯器]** 的 **[一般]** 頁面上，選取下列選項：  
  
    1.  針對 **[ResultSet]**，選取 **[單一資料列]**。  
  
    2.  將有效的連接設定到來源資料庫。  
  
    3.  針對 **[SQLSourceType]**，選取 **[直接輸入]**。  
  
    4.  針對 **[SQLStatement]**，輸入下列 SQL 陳述式：  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  此範例中的 `else` 子句會傳遞開始日期和時間的 Null 值，藉以產生變更資料之初始載入的查詢。 此範例不處理啟用異動資料擷取前所進行之變更也必須上傳到資料倉儲的狀況。  
  
3.  在 [執行 SQL 工作編輯器] 的 [參數對應] 頁面上，進行下列對應：  
  
    1.  將 DataReady 變數對應到參數 0。  
  
    2.  將 ExtractStartTime 變數對應到參數 1。  
  
    3.  將 ExtractEndTime 變數對應到參數 2。  
  
4.  在 [執行 SQL 工作編輯器] 的 [結果集] 頁面上，將 [結果名稱] 對應到 SqlDataQuery 變數。  
  
     [結果名稱] 是所傳回之單一資料行的名稱，也就是 SqlDataQuery。  
  
 上一個程序會利用輸入參數的硬式編碼字串值，設定可準備查詢字串的工作。 下列程式碼為此種查詢字串的範例：  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>加入資料流程工作  
 設計封裝之控制流程的最後一個步驟是加入「資料流程」工作。  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>加入資料流程工作並完成控制流程  
  
-   在 [控制流程] 索引標籤上，加入「資料流程」工作，然後連接串連查詢字串的工作。  
  
## <a name="next-step"></a>下一個步驟  
 準備查詢字串並設定「資料流程」工作後，下一個步驟是建立將從資料庫擷取變更資料的資料表值函式。  
  
 **下一個主題：**[建立函式以擷取變更資料](create-the-function-to-retrieve-the-change-data.md)  
  
  
