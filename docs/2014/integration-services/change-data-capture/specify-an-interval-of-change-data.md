---
title: 指定變更資料的間隔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2c5509699945db857bd0b763192c7aea21ac90da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771201"
---
# <a name="specify-an-interval-of-change-data"></a>指定變更資料的間隔
  在執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的控制流程中，第一個工作是計算變更間隔的端點。 這些端點是 `datetime` 值，而且將會以封裝變數儲存，以便稍後在封裝中使用。  
  
> [!NOTE]  
>  如需設計控制流程之完整程序的描述，請參閱[異動資料擷取 &#40;SSIS&#41;](change-data-capture-ssis.md)。  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>設定端點的封裝變數  
 設定「執行 SQL」工作以計算端點前，必須先定義儲存端點的封裝變數。  
  
#### <a name="to-set-up-package-variables"></a>設定封裝變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **[變數]** 視窗中，建立下列變數：  
  
    1.  建立具有 `datetime` 資料類型的變數，以保存間隔的起始點。  
  
         這個範例會使用變數名稱 ExtractStartTime。  
  
    2.  建立具有 `datetime` 資料類型的另一個變數，以保存間隔的結束點。  
  
         這個範例會使用變數名稱 ExtractEndTime。  
  
 如果您要在主要封裝中，計算執行多個子封裝的端點，您可以使用「父封裝變數」組態，將這些變數的值傳遞到每個子封裝。 如需詳細資訊，請參閱 [執行封裝工作](../control-flow/execute-package-task.md) 和 [在子封裝中使用變數和參數的值](../use-the-values-of-variables-and-parameters-in-a-child-package.md)。  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>計算變更資料的起始點和結束點  
 設定間隔端點的封裝變數後，您可以計算這些端點的實際值，然後將這些值對應到對應的封裝變數。 這些端點都是 `datetime` 值，因此您必須使用可以計算或處理 `datetime` 值的函數。 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式語言和 Transact-SQL 都有可以使用 `datetime` 值的函數：  
  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式語言中，使用 `datetime` 值的函數  
 -   [DATEADD &#40;SSIS 運算式&#41;](../expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF &#40;SSIS 運算式&#41;](../expressions/datediff-ssis-expression.md)  
  
-   [DATEPART &#40;SSIS 運算式&#41;](../expressions/datepart-ssis-expression.md)  
  
-   [DAY &#40;SSIS 運算式&#41;](../expressions/day-ssis-expression.md)  
  
-   [GETDATE &#40;SSIS 運算式&#41;](../expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE &#40;SSIS 運算式&#41;](../expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH &#40;SSIS 運算式&#41;](../expressions/month-ssis-expression.md)  
  
-   [YEAR &#40;SSIS 運算式&#41;](../expressions/year-ssis-expression.md)  
  
 在 Transact-SQL 中，使用 `datetime` 值的函數  
 [日期和時間資料類型與函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)。  
  
 使用其中任何一個 `datetime` 函數計算端點前，您必須判斷間隔是否已經固定，而且是否定期發生。 一般而言，您會想要將來源資料表中發生的變更定期套用到目的地資料表。 例如，您可能會想要每小時、每天，或每週套用一次這些變更。  
  
 了解您的變更間隔是固定還是比較隨機後，您就可以計算端點：  
  
-   **計算開始日期和時間**。 您可以使用上次載入的結束日期和時間當做目前的開始日期和時間。 如果您將固定間隔用於累加式載入，您可以使用 Transact-SQL 或 `datetime` 運算式語言的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 函數來計算這個值。 否則，您可能需要保存執行之間的端點，並使用「執行 SQL」工作或「指令碼」工作來載入前一個端點。  
  
-   **計算結束日期和時間**。 如果您將固定間隔用於累加式載入，計算目前的結束日期和時間當做開始日期和時間的位移。 同樣地，您可以使用 Transact-sql 或`datetime` [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]運算式語言的函數來計算此值。  
  
 在下列程序中，變更間隔會使用固定間隔，並假設累加式載入封裝是每天執行而沒有例外。 否則，將會遺失遺漏間隔的變更資料。 間隔的起點是前天的午夜，也就是在前 24 到 48 小時之間。 間隔的結束點是昨天的午夜，也就是昨天晚上，前 0 到 24 小時之間。  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>計算擷取間隔的起點和結束點  
  
1.  在「 **設計師」的** [控制流程] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 索引標籤上，將「執行 SQL」工作加入到封裝中。  
  
2.  開啟 **[執行 SQL 工作編輯器]** 然後在編輯器的 **[一般]** 頁面上，選取下列選項：  
  
    1.  針對 **[ResultSet]** ，選取 **[單一資料列]** 。  
  
    2.  將有效的連接設定到來源資料庫。  
  
    3.  針對 **[SQLSourceType]** ，選取 **[直接輸入]** 。  
  
    4.  針對 **[SQLStatement]** ，輸入下列 SQL 陳述式：  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  在 **[執行 SQL 工作編輯器]** 的 **[結果集]** 頁面上，將 ExtractStartTime 結果對應到 ExtractStartTime 封裝變數，並將 ExtractEndTime 結果對應到 ExtractEndTime 封裝變數。  
  
    > [!NOTE]  
    >  當您使用運算式來設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 變數的值時，每次存取變數的值時，就會評估該運算式。  
  
## <a name="next-step"></a>後續步驟  
 計算變更範圍的起點和結束點後，下一個步驟是判斷變更資料是否就緒。  
  
 **下一個主題：** [判斷變更資料是否就緒](determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>另請參閱  
 [在封裝中使用變數](../use-variables-in-packages.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)   
 [執行 SQL 工作](../control-flow/execute-sql-task.md)   
 [指令碼工作](../control-flow/script-task.md)  
  
  
