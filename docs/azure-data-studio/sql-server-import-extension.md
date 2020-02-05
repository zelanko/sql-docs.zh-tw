---
title: SQL Server 匯入延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure Data Studio 的 SQL Server 匯入延伸模組 (預覽)
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959126"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 匯入延伸模組 (預覽)

SQL Server 匯入延伸模組 (預覽) 會將 .txt 和 .csv 檔案轉換成 SQL 資料表。 此精靈利用稱為 [Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) 的 Microsoft 研究架構，以最少使用者輸入的智慧方式剖析檔案。 這是用於資料整頓的強大架構，也是提供 Microsoft Excel 中快速填滿功能的相同技術

若要深入了解此功能的 SSMS 版本，您可以閱讀[這篇文章](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)。


## <a name="install-the-sql-server-import-extension"></a>安裝 SQL Server 匯入延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視]  功能表中的 [延伸模組]  。
2. 選取可用的延伸模組，檢視詳細資料。

   ![匯入延伸模組管理員](media/sql-server-import-extension/import-wizard-install.png)

1. 選取您想要的延伸模組並加以**安裝**。
2. 選取 [重新載入]  ，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。

## <a name="start-import-wizard"></a>啟動匯入精靈

1. 若要啟動 SQL Server 匯入，請先在 [伺服器] 索引標籤中建立伺服器連線。
2. 建立連線之後，向下切入至您要匯入檔案到 SQL 資料表的目標資料庫。
3. 以滑鼠右鍵按一下此資料庫，然後按一下 [匯入精靈]  。
    ![開啟 [匯入精靈]](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>匯入檔案
1. 當您按一下滑鼠右鍵啟動精靈時，會自動填入伺服器和資料庫。 如果有其他使用中的連線，您可以在下拉式清單中選取。 
    
    按一下 [瀏覽]  ，選取檔案。 資料表名稱應該會根據檔名自動填入，但您也可以自行變更。

    結構描述預設為 dbo，但您可以變更。 按 [下一步]  繼續進行。
    ![輸入檔](media/sql-server-import-extension/import-wizard-input-file.png)
1. 精靈會根據前 50 個資料列產生預覽。 除了確認資料是否正確之外，不需要在此頁面上執行其他動作。 按 [下一步]  繼續進行。
    ![開啟 [匯入精靈]](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 在此頁面上，您可以變更資料行名稱、資料類型、是否為主索引鍵，或是否允許 Null。 如有需要，您可以進行多次變更。 按一下 [匯入資料]  繼續進行。
    ![開啟 [匯入精靈]](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 此頁面提供所選動作的摘要。 您也可以查看資料表是否成功插入。 

    如果您需要進行變更，您可以按一下 [完成]、[上一步]  ，或按一下 [匯入新檔案]  快速匯入另一個檔案。
    ![開啟 [匯入精靈]](media/sql-server-import-extension/import-wizard-summary.png)
1. 重新整理目標資料庫，或在資料表名稱上執行 SELECT 查詢，確認您的資料表是否成功匯入。

## <a name="next-steps"></a>後續步驟
- 若要深入了解 [匯入精靈]，請閱讀[部落格文章](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)。
- 若要深入了解 PROSE，請閱讀[文件](https://microsoft.github.io/prose/)。
