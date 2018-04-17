---
title: 使用 Foreach 迴圈容器執行 Excel 檔案和資料表迴圈 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3a6bda13eb448dd8071908de58206b31fc003181
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="loop-through-excel-files-and-tables-by-using-a-foreach-loop-container"></a>使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表
  此主題的程序描述如何使用「Foreach 迴圈」容器搭配適當列舉值，循環使用資料夾中的 Excel 活頁簿，或循環使用 Excel 活頁簿中的資料表。  

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>使用 Foreach 檔案列舉值循環使用 Excel 檔案  
  
1.  建立字串變數，用以在迴圈的每個反覆運算上接收目前的 Excel 路徑和檔案名稱 為了避免驗證問題，請指派有效的 Excel 路徑和檔案名稱當做變數的初始值 (此程序後面顯示的範例運算式會使用 `ExcelFile`變數名稱)。  
  
2.  (選擇性) 建立另一個字串變數，用以保存 Excel 連接字串之 [擴充屬性] 引數的值。 這個引數包含一系列的值，這些值指定 Excel 版本並決定第一個資料列是否包含資料行名稱，以及是否使用匯入模式。 (此程序後面顯示的範例運算式會使用變數名稱 `ExtProperties`，以及 "`Excel 8.0;HDR=Yes`" 的初始值)。  
  
     如果您沒有針對 [擴充屬性] 引數使用變數，就必須手動將它加入至包含連接字串的運算式。  
  
3.  將 Foreach 迴圈容器加入 [控制流程] 索引標籤。如需如何設定 Foreach 迴圈容器的資訊，請參閱[設定 Foreach 迴圈容器](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)。  
  
4.  在 [Foreach 迴圈編輯器] 的 [集合] 頁面上，選取 Foreach 檔案列舉值、指定 Excel 活頁簿所在位置的資料夾，並指定檔案篩選 (通常是 *.xls)。  
  
5.  在 [變數對應] 頁面上，將 [索引 0] 對應至使用者自訂的字串變數，該變數將接收迴圈每個反覆運算上目前的 Excel 路徑和檔案名稱。 (此程序後面顯示的範例運算式會使用 `ExcelFile` 變數名稱)。  
  
6.  關閉 [Foreach 迴圈編輯器]。  
  
7.  如[加入、刪除或共用封裝中的連線管理員](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)中所述，將 Excel 連線管理員加入封裝。 選取現有的 Excel 活頁簿檔案做為要連接的檔案，以避免驗證錯誤。  
  
    > [!IMPORTANT]  
    >  為了避免在設定使用此 Excel 連線管理員的工作和資料流程元件時發生驗證錯誤，請在 [Excel 連線管理員編輯器] 中選取現有的 Excel 活頁簿。 在設定了 **ConnectionString** 屬性的運算式之後 (如下列步驟所述)，連線管理員就不會在執行階段使用這個活頁簿。 在您建立和設定封裝之後，就可以在 [屬性] 視窗中清除 **ConnectionString** 屬性的值。 不過，如果您要清除這個值，除非執行「ForEach 迴圈」，否則 Excel 連接管理員的連接字串屬性將不再有效。 因此，您必須將使用連線管理員的工作或封裝的 **DelayValidation** 屬性設為 [True]，以避免驗證錯誤。  
    >   
    >  您也必須將 [False] 的預設值用於 Excel 連線管理員的 **RetainSameConnection** 屬性。 如果您將此值變更為 [True]，迴圈的每個反覆運算都會繼續開啟第一個 Excel 活頁簿。  
  
8.  選取新的 Excel 連線管理員，在 [屬性] 視窗中按一下 **Expressions** 屬性，然後按一下省略符號。  
  
9. 在 [屬性運算式編輯器] 中，選取 **ConnectionString** 屬性，然後按一下省略符號。  
  
10. 在「運算式產生器」中，輸入下列運算式：  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     請注意，逸出字元 "\\" 是用來逸出括住 [擴充屬性] 引數之值的內部雙引號。  
  
     [擴充屬性] 引數不是選擇性的。 如果您沒有使用變數來包含其值，就必須手動將它加入至運算式，如 Excel 2003 檔案的下列範例所示。  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 8.0"  
    ```  
  
11. 在「Foreach 迴圈」容器中建立工作，以便使用 Excel 連接管理員在符合指定之檔案位置和模式的每個 Excel 活頁簿上執行相同的作業。  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>使用 Foreach ADO.NET 結構描述資料列集列舉值來循環使用 Excel 資料表  
  
1.  建立會使用 Microsoft Jet OLE DB 提供者連接到 Excel 活頁簿之 ADO.NET 連接管理員。 在 [連線管理員] 對話方塊的 [全部] 頁面上，確定您輸入 Excel 8.0 做為 Extended Properties 屬性的值。 如需詳細資訊，請參閱 [加入、刪除或共用封裝中的連線管理員](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)。  
  
2.  建立會接收迴圈每個反覆運算上目前資料表名稱的字串變數。  
  
3.  將 Foreach 迴圈容器加入 [控制流程] 索引標籤。如需如何設定Foreach 迴圈容器的資訊，請參閱[設定 Foreach 迴圈容器](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)。  
  
4.  在 [Foreach 迴圈編輯器] 的 [集合] 頁面上，選取 [Foreach ADO.NET 結構描述資料列集] 列舉值。  
  
5.  選取您先前建立的 ADO.NET 連線管理員作為 [連接] 的值。  
  
6.  選取 [資料表] 作為 [結構描述] 的值。  
  
    > [!NOTE]  
    >  Excel 活頁簿中資料表清單包含活頁簿 (具有 $ 後置詞) 及具名範圍。 如果您必須只篩選清單中的活頁簿或具名範圍，必須在指令碼工作中寫入這個用途的自訂程式碼。 如需詳細資訊，請參閱[以指令碼工作處理 Excel 檔案](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)。  
  
7.  在 [變數對應] 頁面上，將 [索引 2] 對應至先前建立的字串變數，以保留目前資料表的名稱。  
  
8.  關閉 [Foreach 迴圈編輯器]。  
  
9. 在「Foreach 迴圈」容器中建立工作，以便使用 Excel 連接管理員在指定之活頁簿中的每個 Excel 資料表上執行相同的作業。 如果您使用指令碼工作檢查列舉的資料表名稱，或者用來處理每個資料表，請記得將字串變數加入指令碼工作的 ReadOnlyVariables 屬性中。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)  
 [設定 Foreach 迴圈容器](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [新增或變更屬性運算式](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Excel 來源](../../integration-services/data-flow/excel-source.md)   
 [Excel 目的地](../../integration-services/data-flow/excel-destination.md)   
 [以指令碼工作處理 Excel 檔案](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
