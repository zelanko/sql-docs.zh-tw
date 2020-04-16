---
title: 基於文字查詢設計器使用者介面 ( F)微軟文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 340040a0806a87d55582356d085ab924e25b6a48
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388672"
---
# <a name="text-based-query-designer-user-interface"></a>以文字為基礎的查詢設計工具使用者介面
  使用以文字為基礎的查詢設計工具，可透過資料來源支援的查詢語言來指定查詢、執行查詢，並在設計階段檢視結果。 您可以指定多個 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、自訂資料處理延伸模組的查詢或命令語法，以及指定為運算式的查詢。 以文字為基礎的查詢設計工具不會前置處理查詢，而且可以容納各種查詢語法，所以這是許多資料來源類型的預設查詢設計工具。

 以文字為基礎的查詢設計工具會顯示一個工具列及以下兩個窗格：

-   **查詢**顯示查詢文本、表名稱或儲存過程名稱。

-   **結果** ：顯示在設計階段執行查詢的結果。

## <a name="text-based-query-designer-toolbar"></a>以文字為基礎的查詢設計工具工具列
 以文字為基礎的查詢設計工具為所有的命令類型提供了單一工具列。 下表列出工具列上的每一個按鈕以及該按鈕的功能。

|按鈕|描述|
|------------|-----------------|
|**[當成文字編輯]**|在以文字為基礎的查詢設計工具和圖形化查詢設計工具之間切換。 並非所有的資料來源類型都支援圖形化查詢設計工具。|
|[匯入]****|從檔案或報表匯入現有的查詢。 只支援 sql 和 rdl 檔案類型。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|
|![執行查詢](../analysis-services/media/rsqdicon-run.gif "執行查詢")|執行查詢，並將結果集顯示在 [結果] 窗格中。|
|**命令類型**|選取 [Text]****、[StoredProcedure]**** 或 [TableDirect]****。 如果預存程序含有參數，當您按一下工具列上的 [執行]**** 時，便會顯示 [定義查詢參數]**** 對話方塊，您可以依照需要填入值。 請注意,如果存儲過程返回多個結果集,則僅使用第一個結果集來填充數據集。<br /><br /> 對於命令類型的支援會依資料來源類型而有所不同。 例如，只有 OLE DB 和 ODBC 支援 [TableDirect]****。|

### <a name="command-type-text"></a>Text 命令類型
 當您建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料集時，報表設計師預設會顯示圖形化查詢設計工具。 若要切換到文字型查詢設計工具，請按一下工具列上的 [當成文字編輯]**** 切換按鈕。 以文字為基礎的查詢設計工具會顯示兩個窗格：[查詢] 窗格和 [結果] 窗格。 下圖會標示出各個窗格。

 ![一般查詢設計工具，適用於關聯式資料查詢](../analysis-services/media/rsqd-dsaw-sql-generic.gif "一般查詢設計工具，適用於關聯式資料查詢")

 下表會描述各個窗格的功能。

|窗格|函式|
|----------|--------------|
|查詢|顯示 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢文字。 使用此窗格，即可撰寫或編輯 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢。|
|結果|顯示查詢的結果。 若要執行查詢，請以滑鼠右鍵按一下任何窗格，然後按一下 [執行]****，或是按一下工具列上的 [執行]**** 按鈕。|

#### <a name="example"></a>範例
 下列查詢會從 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫的 `Contact` 資料表傳回姓氏清單。

```
SELECT LastName FROM Person.Person;
```

 您可以使用 Text 命令類型的任何 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式，包括 `EXEC` 陳述式在內。 以下查詢調用[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]存儲`uspGetEmployeeManagers`過程 ,並返回具有標識號 1 的員工的命令鏈。

```
EXEC uspGetEmployeeManagers 1;
```

 當您按一下工具列上的 [執行]**** 時，[查詢]**** 窗格中的命令便會執行，而且結果會顯示在 [結果]**** 窗格中。

### <a name="command-type-storedprocedure"></a>StoredProcedure 命令類型
 當您選取 [命令類型] [StoredProcedure]**** 時，文字型查詢設計工具會顯示兩個窗格：[查詢] 窗格和 [結果] 窗格。 請在 [查詢] 窗格內輸入預存程序名稱，然後按一下工具列上的 [執行]****。 [定義查詢參數] 對話方塊隨即開啟。 為此預存程序輸入參數值。 將會針對每一個預存程序參數建立報表參數。

#### <a name="example"></a>範例
 下列查詢會呼叫 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 預存程序 `uspGetEmployeeManagers`。 當您執行查詢時，必須為員工識別碼參數輸入值。

```
uspGetEmployeeManagers;
```

### <a name="command-type-tabledirect"></a>TableDirect 命令類型
 當您選取 [命令類型] [TableDirect]**** 時，文字型查詢設計工具會顯示兩個窗格：[查詢] 窗格和 [結果] 窗格。 當您輸入資料表並按一下 [執行]**** 按鈕時，便會傳回該資料表的所有資料行。

#### <a name="example"></a>範例
 下列查詢會傳回 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中所有客戶的結果集。

 `Sales.Customer`

 當您輸入表名 Sales.Customer 時,它等效[!INCLUDE[tsql](../includes/tsql-md.md)]於建立`SELECT * FROM Sales.Customer;`敘述 。

## <a name="see-also"></a>另請參閱
 [報表設計器 SQL 伺服器資料工具中的查詢設計工具&#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)[報表生成器和共享資料集&#40;報表生成器和共享資料集&#40;報表生成器和共享資料集](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) [&#41;&#40;sSRS&#41;](report-data/sql-server-connection-type-ssrs.md) OLE DB[連接類型&#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md) [ODBC 連接類型&#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md)[報表嵌入資料集和共用資料集&#40;報表產生器和 SSRS](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) RS&#41;[報告設計器配置檔](report-server/rsreportdesigner-configuration-file.md)


