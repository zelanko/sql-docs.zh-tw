---
description: 查詢和檢視設計工具表示聯結的方式 (Visual Database Tools)
title: 查詢設計工具和檢視表設計師的聯結表示方式
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: a1d8686e1502fab121e49abed19f8f01488d22b7
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439352"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>查詢和檢視設計工具表示聯結的方式 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 如果資料表是聯結的，[查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)將在[圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)中以圖形表示該聯結，並在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中使用 SQL 語法。  
  
## <a name="diagram-pane"></a>圖表窗格  
[查詢和檢視設計師] 會在 [圖表] 窗格中，顯示與聯結相關之資料行之間的聯結線。 查詢和檢視設計師可顯示每個聯結狀況的聯結線。 例如，下列圖示即說明兩個聯結的資料表之間的聯結線：  
  
![聯結線會顯示兩個資料表之間的關聯性](../../ssms/visual-db-tools/media/dv3wbig.gif "聯結線會顯示兩個資料表之間的關聯性")  
  
如果資料表使用一個以上的聯結條件來進行聯結，查詢和檢視設計師將顯示多重聯結線，如下列範例所示：  
  
![使用一個以上聯結條件所聯結的資料表](../../ssms/visual-db-tools/media/dv3w9n1.gif "使用一個以上聯結條件所聯結的資料表")  
  
如果聯結線並未顯示 (例如，代表資料表或表格化物件的矩形被最小化，或該聯結使用運算式)，查詢和檢視設計師將在代表資料表或表格化物件的矩形標題列上放置聯結線。  
  
聯結線中間的圖示形狀即表示資料表或表格化物件的聯結方式。 如果聯結子句使用等號 (=) 以外的運算子，該運算子將出現在聯結線圖示中。 下表將列出可顯現於聯結線中的圖示。  
  
|**聯結線圖示**|**說明**|  
|----------------------|-------------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbih.gif":::|內部聯結 (使用等號建立)。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbii.gif":::|使用「大於」運算子的內部聯結。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbij.gif":::|外部聯結，將包括左邊資料表的所有資料列，即使該資料表在相關資料表並沒有相符項目。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbik.gif":::|外部聯結，將包括右邊資料表的所有資料列，即使該資料表在相關資料表中並沒有相符項目。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbil.gif":::|完整的外部聯結，將同時包括兩邊資料表的所有資料列，即使該資料表在相關資料表中並沒有相符項目。|  
  
聯結線結束部分的符號可表示聯結的類型。 下表即列出聯結的類型和聯結線結束部分所顯示的圖示。  
  
|**聯結線結束部分所顯示的圖示**|**聯結類型**|  
|---------------------------------|--------------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbim.gif":::|一對一聯結。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbin.gif":::|一對多聯結。|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbio.gif":::|查詢和檢視設計師無法決定聯結類型。 當您手動建立某個聯結後，常會發生這種情況。|  
  
## <a name="sql-pane"></a>SQL 窗格  
SQL 陳述式有數種方法來表示聯結。 確切的語法則視您使用的資料庫和您定義聯結的方式而定。  
  
聯結資料表的語法選項包括：  
  
-   **FROM 子句的 JOIN 限定詞** 。   關鍵字 INNER 和 OUTER 將指定聯結類型。 這為 ANSI 92 SQL 的標準語法。  
  
    例如，如果您根據每個資料表中的 `publishers` 資料行來聯結 `pub_info` 和 `pub_id` 資料表，將產生以下 SQL 陳述式：  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
    如果您要建立外部聯結，LEFT OUTER 或 RIGHT OUTER 等字樣將取代 INNER 一字。  
  
-   **WHERE 子句將比較兩個資料表中的資料行** 。   如果資料庫不支援 JOIN 語法 (或者您自行輸入該語法)，則將出現 WHERE 子句。 如果在 WHERE 子句中建立聯結，FROM 子句將同時出現這兩個資料表名稱。  
  
    例如，下列陳述式即聯結了 `publishers` 和 `pub_info` 資料表。  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[聯結對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
