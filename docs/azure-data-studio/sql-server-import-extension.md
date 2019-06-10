---
title: SQL Server 匯入擴充功能
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure 資料 Studio 的 SQL Server 匯入擴充功能 （預覽）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 5866e70945e7a507c0a8887abf006858d37c2bf0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798013"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 匯入擴充功能 （預覽）

SQL Server 匯入擴充功能 （預覽） 會將.txt 或.csv 檔案轉換成 SQL 資料表。 此精靈會利用 Microsoft Research 架構，稱為[Program Synthesis using 範例 (PROSE)](https://microsoft.github.io/prose/)以智慧方式剖析具有最少的使用者輸入的檔案。 它是功能強大的架構，用於資料處理，而且相同的技術，提供在 Microsoft Excel 中 Flash 填滿

若要深入了解這項功能的 SSMS 版本，您可以閱讀[這篇文章](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)。


## <a name="install-the-sql-server-import-extension"></a>安裝 SQL Server 匯入擴充功能

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 選取可用的擴充功能以檢視其詳細資料。

   ![匯入延伸模組管理員](media/sql-server-import-extension/import-wizard-install.png)

1. 選取您想要的延伸模組並**安裝**它。
2. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。

## <a name="start-import-wizard"></a>啟動匯入精靈

1. 若要啟動 SQL Server 匯入，首先請在 [伺服器] 索引標籤中的伺服器的連接。
2. 您建立連線之後，向下鑽研至您想要將檔案匯入的 SQL 資料表的目標資料庫。
3. 以滑鼠右鍵按一下資料庫，然後按一下 [**匯入精靈]** 。
    ![開啟匯入精靈](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>匯入檔案
1. 當您以滑鼠右鍵按一下來啟動精靈時，在伺服器和資料庫都已自動填入。 如果沒有其他作用中的連線，您可以選取下拉式清單中。 
    
    按一下 選取檔案**瀏覽。** 它應該自動填入的資料表名稱會根據檔案名稱，但您也可以變更它自己。

    根據預設，結構描述就是 dbo，但您可以加以變更。 按 **[下一步]** 繼續進行。
    ![輸入的檔](media/sql-server-import-extension/import-wizard-input-file.png)
1. 精靈會產生預覽，根據前 50 個資料列。 沒有任何額外的動作，在此頁面上其他與驗證資料看起來正確。 按 **[下一步]** 繼續進行。
    ![開啟匯入精靈](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 在此頁面上，您可以變更資料行名稱，資料類型，它是主索引鍵，還是允許 null。 您可以讓數目的變更。 按一下 **匯入資料**以繼續。
    ![開啟匯入精靈](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 此頁面可讓選擇的動作的摘要。 您也可以查看您的資料表插入成功與否。 

    您可以按一下**完成之後上, 一步**如果您需要進行變更，或是**匯入新的檔案**快速匯入另一個檔案。
    ![開啟匯入精靈](media/sql-server-import-extension/import-wizard-summary.png)
1. 請確認是否您已成功匯入資料表的重新整理您的目標資料庫或資料表名稱上執行 SELECT 查詢。

## <a name="next-steps"></a>後續步驟
- 若要深入了解匯入精靈，請閱讀[部落格文章](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)。
- 若要深入了解 PROSE，閱讀[文件。](https://microsoft.github.io/prose/)
