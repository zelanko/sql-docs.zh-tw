---
title: 將範例資料加入至設計模式中的 DirectQuery 模型 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ca4c4c2a00eed80e709602084cf5de427134977
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041632"
---
# <a name="add-sample-data-to-a-directquery-model-in-design-mode"></a>在設計模式中將範例資料加入 DirectQuery 模型中
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
 在 DirectQuery 模式中，資料表資料分割可用來建立模型設計期間所使用的範例資料子集，或建立完整資料檢視的替代品。
 
 部署 DirectQuery 表格式模型時，每個資料表只允許有一個資料分割，且該資料分割必須是完整資料檢視。 任何其他的資料分割都是完整資料檢視或範例資料的替代品。 在本主題中，我們將描述如何使用資料子集來建立範例資料分割。
 
 依預設，在 SSDT 中設計 DirectQuery 模式的表格式模型時，模型的工作資料庫不包含任何資料。 每個資料表都有一個預設的資料分割，而且此資料分割會將所有查詢導向至資料來源。 
  
不過，您可以將較少量的範例資料加入模型的工作資料庫，以供設計階段使用。 範例資料僅在設計期間使用，並透過範例資料分割上的查詢來指定。 它會在記憶體中與模型一起快取。 這有助於您隨處都可驗證模型決策，而不會影響資料來源。 您可以在 SQL Server Data Tools (SSDT) 中 (或從其他連接到工作空間資料庫的用戶端應用程式)，使用 [在 Excel 中進行分析]，透過範例資料集來測試模型決策。  
  
> [!TIP]  
>  即使是在空模型的 DirectQuery 模式中，您一律可以檢視每個資料表的小型內建資料列集。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，按一下 [資料表] > [資料表屬性] 以檢視 50 列的資料集。  
  
## <a name="create-a-sample-partition"></a>建立範例資料分割
 這些指示是在建立或升級至 1200年或更高的相容性層級的表格式模型。 較低相容性層級的模型會使用不同的屬性來取得快取資料。 如需屬性描述，請參閱 [在 SSMS 中啟用 DirectQuery 模式](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md) 。  
  
1.  在 SQL Server Data Tools 的圖表檢視或資料檢視中，按一下事實資料表以開啟其屬性頁面。 事實資料表提供模型中彙總的數值資料以及量值。 您可能會擁有一個以上的表格。  
  
2.  按一下 [資料表] > [屬性] 以開啟 [資料分割管理] 對話方塊。  
  
    請注意預設資料分割是 **（直接查詢）\<資料表名稱 >**。 這是完整資料檢視。 請勿刪除此資料分割。 部署模型時，將會使用此資料分割。  
  
4.  選取資料分割，然後按一下 [複製]。  

    這會建立預設資料分割的複本，但此複本將會包含您在查詢中指定的範例資料。 例如：
  
     ![ssas_tabularproject_copypartition](../../analysis-services/tabular-models/media/ssas-tabularproject-copypartition.jpg "ssas_tabularproject_copypartition")  
  
5.  選取複製的資料分割，然後按一下 [SQL 查詢編輯器] 按鈕加入篩選。 撰寫模型時，可減少範例資料大小。 例如，如果從 AdventureWorksDW 選取 **FactInternetSales**，您的篩選可能如下所示：  
  
    ```  
    SELECT [dbo].[FactInternetSales].* FROM [dbo].[FactInternetSales]  
    JOIN DimSalesTerritory as ST  
    ON ST.SalesTerritoryKey = FactInternetSales.SalesTerritoryKey  
    WHERE ST.SalesTerritoryGroup='North America';  
    ```  
  
6.  按一下 [驗證] 檢查是否有語法錯誤。  
  
     請注意，在 DirectQuery 模式中，除了 [資料分割] 對話方塊上的 [新增]、[複製] 和 [刪除] 按鈕外，另外還有切換按鈕可以交替讀取 [設定為 Sample] 或 [設為 DirectQuery]。  
  
     只有一個資料分割可以作為 DirectQuery 資料分割。 您可以選取為資料表定義的任何資料分割，然後按一下 [設定為 Sample] 來進行控制。  
  
7.  處理資料表。  
  


  
  
