---
title: 虛擬化 SQL Server 2019 CTP 2.0 中的外部資料 | Microsoft Docs
description: 此頁面詳述針對 CSV 檔案使用 [建立外部資料表精靈] 的步驟
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6a8ce50e4e359c8ce8dc2b0015300f9a7afb88d1
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710602"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>搭配使用外部資料表精靈與 CSV 檔案

SQL Server 2019 也可讓您虛擬化 HDFS 中 CSV 檔案的資料。  此程序允許將資料保留在其原始位置，但您可以在 SQL Server 執行個體中**虛擬化**資料，以在該處查詢它，如同 SQL Server 中的任何其他資料表。 這項功能會將 ETL 程序的需求降到最低。 這只要使用 Polybase 連接器就能做到。 如需資料虛擬化的詳細資訊，請參閱[開始使用 PolyBase](polybase-guide.md) 文件。

## <a name="prerequisite"></a>必要條件

從 CTP 2.4 開始，依預設已不會在巨量資料叢集中建立資料集區和存放集區外部資料來源。 使用精靈之前，請使用下列 Transact-SQL 查詢在您的目標資料庫中建立預設的 **SqlStoragePool** 外部資料來源。 請務必先將查詢的內容變更為您的目標資料庫。

```sql
-- Create default data sources for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://controller-svc/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="launch-the-external-table-wizard"></a>啟動 [外部資料表精靈]

使用 IP 位址連線到 HDFS 根目錄。 在 [物件總管] 中展開所有項目。 然後選取您想要將其資料虛擬化到現有 SQL Server 執行個體的其中一個來源 CSV。 以滑鼠右鍵按一下檔案，然後從操作功能表選取 [Create External Table From CSV File] \(從 CSV 檔案建立外部資料表\)  。 您也可以從 HDFS 中資料夾內的 CSV 檔案建立外部資料表，但前提是這些檔案所在資料夾遵循相同的結構描述。 如此可在資料夾層級虛擬化資料，而不需要處理個別檔案並透過合併資料來取得聯結的結果集。 這會啟動 [虛擬化資料精靈]。 您也可以鍵入 Ctrl+Shift+P (在 Windows 中) 和 Cmd+Shift+P (在 Mac 中)，以從命令選擇區啟動 [虛擬化資料精靈]。

![虛擬化資料精靈](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>連線到 SQL Server 主要執行個體

您也可以在這裡指定要使用 IP、連接埠和認證資訊連線的 SQL 主要執行個體。 之前儲存的連線可透過 [Active SQL Server connections] \(使用中的 SQL Server 連線\)  下拉式清單方塊來存取。 
> [!NOTE]
>如果您使用儲存的連線，則不會封鎖其他防火牆


![選取資料來源](media/data-virtualization/csv-connect-to-master.png)

按一下 [下一步] 繼續精靈中設定資料庫主要金鑰的下一步。

## <a name="select-destination-database"></a>選取目的地資料庫

在此步驟中，您將選擇要虛擬化資料的目的地資料庫。 下拉式清單欄位會包含前一個畫面中所指定 SQL 主要執行個體中所有可接受的資料庫。 您也可以在這裡命名新的外部資料表，並查看它將使用的結構描述。

![建立資料庫主要金鑰](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>預覽資料

在此視窗中，您將能夠預覽 CSV 檔案的前 50 列以進行驗證。

完成檢視預覽後，請按一下 [下一步] 繼續

![外部資料來源認證](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>修改資料行

在下一個視窗中，您將能夠修改想要建立之外部資料表的資料行。 您可以改變資料行名稱、變更資料類型，以及允許可為 Null 的資料列。 

![外部資料來源認證](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>摘要

此步驟提供您選項的摘要。 它會提供 SQL 主要執行個體和提議的外部資料表資訊。 在此步驟中，您可以選擇 [產生指令碼]  (這會以建立外部資料來源語法的 T-SQL 來撰寫指令碼) 或 [建立]  (這會建立外部資料來源物件)。

![摘要畫面](media/data-virtualization/csv-virtualize-data-summary.png)

如果您按一下 [建立]，則可以看到目的地資料庫中所建立的外部資料表。

![外部資料來源](media/data-virtualization/csv-external-data-sources.png)

如果您按一下 [產生指令碼]  ，則會看到建立外部資料來源物件所產生的 T-SQL 查詢。

![產生指令碼](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> [產生指令碼] 應該只顯示在精靈的最後一頁。 目前它會顯示在所有頁面中。

## <a name="next-steps"></a>後續步驟

如需 SQL Server 巨量資料叢集和相關情節的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集？](../../big-data-cluster/big-data-cluster-overview.md)。
