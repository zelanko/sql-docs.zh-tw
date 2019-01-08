---
title: 匯入資料使用原生查詢 (Analysis Services) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c313484b2ee7ff87668cbfdd0b87ed52cdaf98
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523966"
---
# <a name="import-data-by-using-a-native-query"></a>使用原生查詢匯入資料
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
對於表格式 1400年模型，請在 Visual Studio Analysis Services 專案中新的 [取得資料] 功能提供極大的彈性如何混搭您的資料匯入期間。 本文說明建立資料來源的連接，然後再建立原生 SQL 查詢來指定匯入資料。

若要完成本文中所述的工作，請確定您使用最新版的 SSDT。 如果您使用 Visual Studio 2017，請確定您已下載並安裝年 9 月 2017年或更新版本的 Microsoft Analysis Services 專案 VSIX。

[下載和安裝 SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[下載 Microsoft Analysis Services 專案 VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>建立資料來源的連接
如果您還沒有連線到您的資料來源，您需要建立一個。

1. 在 Visual Studio 中 >**表格式模型總管**，以滑鼠右鍵按一下**資料來源**，然後按一下**新的資料來源**。
2. 在 **取得資料**，選取您的資料來源的類型，然後按一下**Connect**。 請遵循連接到您的資料來源所需的所有額外步驟。


## <a name="enter-a-query-as-a-named-expression"></a>輸入查詢做為具名的運算式
1. 在 **表格式模型總管**，以滑鼠右鍵按一下**運算式** > **編輯運算式**。
2. 在 **查詢編輯器**，按一下**查詢** > **新查詢** > **空白查詢**
3. 在公式列中，輸入
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. 在中建立資料表時，**查詢**，以滑鼠右鍵按一下查詢，然後選取**建立新的資料表**。 新的資料表會有同名的查詢。


## <a name="example"></a>範例
此原生查詢建立員工資料表在模型中包含 Dimension.Employee 資料表在資料來源中的所有資料行。

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![查詢編輯器](media/ssas-import-query-example.png)


匯入之後，在模型中建立名為 Employees 資料表。   

![查詢編輯器](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>另請參閱  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [模擬](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
