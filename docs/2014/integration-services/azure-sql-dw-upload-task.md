---
title: Azure SQL DW 上傳工作 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1e5e39f8049a5f2832e7a37381c4d22ef2483b62
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388856"
---
# <a name="azure-sql-dw-upload-task"></a>Azure SQL DW 上傳工作
**Azure SQL DW 上傳工作** 讓 SSIS 套件能夠將本機資料上傳到 Azure SQL 資料倉儲 (DW) 中的資料表。 目前支援的來源資料檔案格式為使用 UTF8 編碼的分隔文字。 上傳程序遵循高效率的 PolyBase 方法。 具體來說，資料會先上傳到 Azure Blob 儲存體，再到 Azure SQL DW。 因此，使用此工作會需要 Azure Blob 儲存體。

若要新增 **Azure SQL DW 上傳工作**，請將其從 SSIS 工具箱拖放到設計工具畫布，然後按兩下或在其上按一下滑鼠右鍵，再按一下 [編輯]  ，即可看到工作編輯器對話方塊。

在 [一般]  頁面上設定下列屬性。

欄位|描述
-----|-----------
LocalDirectory|指定包含要上傳之資料檔案的本機目錄。
Recursively|指定是否要以遞迴方式搜尋子目錄。
FileName|指定名稱篩選，以選取具有特定名稱模式的檔案。 例如 MySheet\*.xsl\* 會包含 MySheet001.xsl 及 MySheetABC.xslx 這類的檔案。
RowDelimiter|指定標示各資料列結尾的字元。
ColumnDelimiter|指定一或多個標示各資料行結尾的字元。 例如 &#124; (縱線字元)、\t (定位字元)、' (單引號)、" (雙引號) 和 0x5c (反斜線)。
IsFirstRowHeader|指定每個資料檔案中的第一個資料列是否包含資料行名稱，而非實際資料。
AzureStorageConnection|指定 Azure 儲存體連線管理員。
BlobContainer|指定要透過 PolyBase 將本機資料上傳及轉送到 Azure DW 的目的 Blob 容器名稱。 如果容器不存在，系統將會建立新容器。
BlobDirectory|指定要透過 PolyBase 將本機資料上傳及轉送到 Azure DW 的目的 Blob 目錄 (虛擬階層式結構)。
RetainFiles|指定是否要保留上傳到 Azure 儲存體的檔案。
CompressionType|指定在將檔案上傳到 Azure 儲存體時要使用的壓縮格式。 本機來源不會受到影響。
CompressionLevel|指定要用於壓縮格式的壓縮層級。
AzureDwConnection|指定 Azure SQL DW 的 ADO.NET 連線管理員。
TableName|指定目的資料表的名稱。 選擇現有的資料表名稱，或選擇 \<新增資料表...> 建立新的資料表。
TableDistribution|指定新資料表的發佈方法。 如果為 **TableName**指定了新的資料表名稱即適用。
HashColumnName|指定用於雜湊表發佈的資料行。 如果為 **TableDistribution** 指定了 **HASH**即適用。

根據您上傳到新資料表或現有資料表，看到的 [對應]  頁面會有所不同。 如果是前者，請設定要對應哪些來源資料行，及其在要建立的目的資料表中對應名稱為何。 如果是後者，請設定來源與目的資料行之間的對應關係。

在 [資料行]  頁面上，為各來源資料行設定資料類型屬性。

[T-SQL]  頁面會顯示用來將資料從 Azure Blob 儲存體上傳到 Azure SQL DW 的 T-SQL。 T-SQL 從其他頁面上的組態自動產生，會在工作執行過程中執行。 您也可以按一下 [編輯]  按鈕以手動編輯產生的 T-SQL，使其符合您的特定需求。 您之後可以按一下 [重設]  按鈕，還原成自動產生的 T-SQL。
