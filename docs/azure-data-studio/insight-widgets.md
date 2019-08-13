---
title: 使用 Azure Data Studio 中的深入解析小工具監視伺服器和資料庫
titleSuffix: Azure Data Studio
description: 了解 Azure Data Studio 中的深入解析小工具
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.openlocfilehash: c1ab90efa97878676b1adc2a62579527407d6ba6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959528"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 中使用深入解析小工具，管理伺服器和資料庫

深入解析小工具會擷取您用來監視伺服器和資料庫的 Transact-SQL (T-SQL) 查詢，並轉換成富有洞察力的視覺效果。

深入解析是您可以新增至伺服器和資料庫監視儀表板的可自訂圖表和圖形。 檢視您伺服器和資料庫的摘要深入解析，然後鑽研更多詳細資料，並啟動您所定義的管理動作。

您可以建置絕佳的伺服器和資料庫管理儀表板，如下列範例所示：

![資料庫儀表板](media/insight-widgets/database-dashboard.png)


若要立即開始建立不同類型的深入解析小工具，請參閱下列教學課程：

- [建置自訂深入解析小工具](tutorial-build-custom-insight-sql-server.md)
- 啟用內建深入解析小工具 
  - [啟用效能監視深入解析](tutorial-qds-sql-server.md)
  - [啟用資料表空間使用量深入解析](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 查詢

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會嘗試避免推出另一種語言或龐大的使用者介面，因此會嘗試盡可能使用需要最少 JSON 設定的 T-SQL。 使用 T-SQL 設定深入解析小工具時，會利用無數個現有的實用 T-SQL 查詢來源，全部都可以轉換成富有洞察力的小工具。

深入解析小工具是由一個或兩個 T-SQL 查詢所組成：
* 「深入解析小工具查詢」  是必要的，而且查詢會傳回小工具中所顯示的資料。
* 只有在您想要建立深入解析詳細資料頁面時，才需要「深入解析詳細資料查詢」  。

此深入解析小工具查詢會定義資料集來轉譯計數、圖表或圖形。 您可以使用深入解析詳細資料查詢，在深入解析詳細資料面板中，以表格格式列出相關的深入解析詳細資訊。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會執行深入解析小工具查詢，並將查詢結果集對應至圖表的資料集，再加以轉譯。 當使用者開啟深入解析的詳細資料時，會執行深入解析詳細資料查詢，並在對話方塊中以格線檢視列出結果。

基本概念是將 T-SQL 查詢撰寫成計數、圖表和圖形小工具的可用資料集。 

## <a name="summary"></a>摘要

T-SQL 查詢及其結果集會決定深入解析小工具的行為。 針對圖表類型撰寫查詢或對應至現有查詢的正確圖表類型，都是在建置有效的深入解析小工具時的重要考量。



## <a name="additional-resources"></a>其他資源
- [查詢編輯器](tutorial-sql-editor.md)

