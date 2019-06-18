---
title: 建立基本資料表報表 (SSRS 教學課程) | Microsoft Docs
ms.date: 04/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af41da75d553794019f1d01c8b8f5bb6aba80622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65103308"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>建立基本資料表報表 (SSRS 教學課程)

在本教學課程中，您可以使用 Visual Studio / SQL Server Data Tools (SSDT) 中的 [報表設計師]  工具。 您可以建立 SQL Server Reporting Services (SSRS) 編頁報表。 報表包含查詢資料表，該資料表是從 AdventureWorks2016 資料庫中的資料建立的。

當您繼續本教學課程時，您將了解如何：
  
- 建立報表專案。
- 設定資料連線。
- 定義查詢。
- 新增資料表資料區域。
- 設定報表格式。
- 群組和總計欄位。
- 預覽報表。
- 選擇性地發佈報表。

## <a name="requirements"></a>需求

您的系統上必須安裝下列元件，才能使用本教學課程：

- [!INCLUDE[msconame-md](../includes/msconame-md.md)] SQL Server 資料庫引擎。  
- SQL Server 2016 Reporting Services 或更新版本 (SSRS)。
- AdventureWorks2016 資料庫。  如需詳細資訊，請參閱 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。
- 安裝適用於 Visual Studio 的 [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md)，以及 Reporting Services 延伸模組可啟用對*報表設計師*的存取。
  
另外，您也必須擁有從 AdventureWorks2016 資料庫擷取資料的唯讀權限。

**完成這個教學課程的估計時間：** 30 分鐘。

## <a name="next-steps"></a>後續步驟

[第 1 課：建立報表伺服器專案 &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)

[第 2 課：指定連接資訊 &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)

[第 3 課：定義資料表報表的資料集 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)

[第 4 課：將資料表加入至報表 &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)

[第 5 課：格式化報表 &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)

[課程 6：加入群組和總計 &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)

## <a name="see-also"></a>另請參閱

[Reporting Services 教學課程](reporting-services-tutorials-ssrs.md) 有其他問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
