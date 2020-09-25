---
title: SQL Server 匯入延伸模組
description: 了解如何安裝和使用適用於 Azure Data Studio 的 SQL Server 匯入延伸模組，這種精靈可將 .txt 和 .csv 檔案轉換成 SQL 資料表。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: caf2b3ee70d2542dc529e83e1e243ff215c644a4
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123033"
---
# <a name="sql-server-import-extension"></a>SQL Server 匯入延伸模組

SQL Server 匯入延伸模組會將 .txt 和 .csv 檔案轉換成 SQL 資料表。 此精靈利用稱為 [Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) 的 Microsoft 研究架構，以最少使用者輸入的智慧方式剖析檔案。 這是一種強大的資料整頓強大架構，Microsoft Excel 的快速填入功能也是使用相同技術

若要深入了解此功能的 SSMS 版本，您可以閱讀[這篇文章](../../relational-databases/import-export/import-flat-file-wizard.md)。

## <a name="install-the-sql-server-import-extension"></a>安裝 SQL Server 匯入延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視] 功能表中的 [延伸模組]。
2. 選取可用的延伸模組，檢視詳細資料。

   ![匯入延伸模組管理員](media/sql-server-import-extension/import-wizard-install.png)

3. 選取您想要的延伸模組並加以**安裝**。
4. 選取 [重新載入]  ，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。

## <a name="start-import-wizard"></a>啟動匯入精靈

1. 若要啟動 SQL Server 匯入，請先在 [伺服器] 索引標籤中建立伺服器連線。
2. 建立連線之後，向下切入至您要匯入檔案到 SQL 資料表的目標資料庫。
3. 以滑鼠右鍵按一下此資料庫，然後選取 [匯入精靈]。

    ![匯入精靈](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>匯入檔案

1. 當您按一下滑鼠右鍵啟動精靈時，會自動填入伺服器和資料庫。 如果有其他使用中的連線，您可以在下拉式清單中選取。 

    選取 [瀏覽] 以選取檔案。 應該會根據檔案名稱自動填入資料表名稱，但也可以自行變更。

    結構描述預設為 dbo，但您可以變更。 選取 [下一步] 繼續進行。

    ![輸入檔](media/sql-server-import-extension/import-wizard-input-file.png)

2. 精靈會根據前 50 個資料列產生預覽。 除了確認資料是否正確之外，不需要在此頁面上執行其他動作。 選取 [下一步] 繼續進行。

    ![預覽資料](media/sql-server-import-extension/import-wizard-preview-data.png)

3. 在此頁面上，您可以變更資料行名稱、資料類型、是否為主索引鍵，或是否允許 Null。 如有需要，您可以進行多次變更。 選取 [匯入資料] 繼續進行。

    ![修改資料行](media/sql-server-import-extension/import-wizard-modify-columns.png)

4. 此頁面提供所選動作的摘要。 您也可以查看資料表是否成功插入。

    如果您需要進行變更，您可以選取 [完成]、[上一步]，或按一下 [匯入新檔案] 快速匯入另一個檔案。

    ![摘要](media/sql-server-import-extension/import-wizard-summary.png)

5. 重新整理目標資料庫，或在資料表名稱上執行 SELECT 查詢，確認您的資料表是否成功匯入。

## <a name="next-steps"></a>後續步驟

- 若要深入了解 [匯入精靈]，請閱讀[部落格文章](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)。
- 若要深入了解 PROSE，請閱讀[文件](https://microsoft.github.io/prose/)。