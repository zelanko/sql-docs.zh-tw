---
title: 虛擬化 SQL Server 2019 CTP 2.0 中的外部資料 | Microsoft Docs
description: 此頁面詳述針對關聯式資料來源使用 [建立外部資料表精靈] 的步驟
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a8f5f55dfa0a569ec88542f819e30d21889997e3
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596669"
---
# <a name="use-the-external-table-wizard-with-relational-data-sources"></a>搭配使用外部資料表精靈與關聯式資料來源

其中一個 SQL Server 2019 CTP 2.0 重要情節是可以虛擬化資料。 此程序允許將資料保留在其原始位置。 您可以在 SQL Server 執行個體中「虛擬化」資料，以在該處查詢它，如同 SQL Server 中的任何其他資料表。 此程序會將 ETL 程序的需求降到最低。 此程序只要使用 PolyBase 連接器就能達成。 如需資料虛擬化的詳細資訊，請參閱[開始使用 PolyBase](polybase-guide.md)。

## <a name="start-the-external-table-wizard"></a>啟動外部資料表精靈

使用在部署指令碼結尾取得的 IP 位址/連接埠號碼 (31433) 來連線至主要執行個體。 展開 [物件總管] 中的 [資料庫] 節點。 然後選取您想要將資料從現有 SQL Server 執行個體虛擬化到其中的其中一個資料庫。 以滑鼠右鍵按一下資料庫，然後選取 [建立外部資料表] 以啟動 [虛擬化資料精靈]。 您也可以從命令選擇區啟動 [虛擬化資料精靈]。 使用 Ctrl+Shift+P (在 Windows 中) 或 Cmd+Shift+P (在 Mac 中)。

![虛擬化資料精靈](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>選取資料來源

如果您已從其中一個資料庫啟動此精靈，則目的地下拉式方塊會自動填入。 您也可以選擇在此頁面上輸入或變更目的地資料庫。 精靈所支援的外部資料來源類型是 SQL Server 和 Oracle。

> [!NOTE]
>根據預設，會醒目提示 SQL Server。


![選取資料來源](media/data-virtualization/select-data-source.png)

選取 [下一步] 繼續進行。

## <a name="create-a-database-master-key"></a>建立資料庫主要金鑰

在此步驟中，您會建立資料庫主要金鑰。 需要建立主要金鑰。 主要金鑰會保護外部資料來源所使用的認證。 選擇主要金鑰的強式密碼。 此外，使用 **BACKUP MASTER KEY** 來備份主要金鑰。 將備份存放在安全且位於異地的位置。

![建立資料庫主要金鑰](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 如果您已經有資料庫主要金鑰，則會限制輸入欄位，而且您可以略過此步驟。 選取 [下一步] 繼續進行。

> [!NOTE]
> 如果您未選擇強式密碼，精靈會在最後一個步驟中執行此作業。 這是已知的問題。

## <a name="enter-external-data-source-credentials"></a>輸入外部資料來源認證

在此步驟中，輸入您的外部資料來源和認證詳細資料，以建立外部資料來源物件。 資料庫物件會使用這些認證連線到資料來源。 輸入外部資料來源的名稱。 例如 Test。 提供外部資料來源 SQL Server 連線詳細資料。 輸入您想要建立外部資料來源的 [伺服器名稱] 和 [資料庫名稱]。

下一個步驟是設定認證。 輸入認證的名稱。 此名稱是資料庫範圍認證，可用來安全地儲存您所建立外部資料來源的登入資訊。 例如 TestCred。 輸入使用者名稱與密碼以連線到資料來源。

![外部資料來源認證](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>外部資料表對應

在下一個頁面上，選取您想要建立外部檢視的資料表。 當您選取父資料庫時，也會包含子資料表。 選取資料表之後，對應資料表會出現在右側。 您可以在這裡進行類型變更。 您也可以變更所選取外部資料表本身的名稱。

![外部資料來源認證](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>若要變更對應檢視，請按兩下另一個選取的資料表。

> [!IMPORTANT]
>外部資料表工具不支援相片類型。 如果建立其中具有相片類型的外部檢視，則會在建立資料表之後出現錯誤。 不過仍然會建立資料表。

## <a name="summary"></a>摘要

此步驟顯示您選項的摘要。 它會提供資料庫範圍認證名稱以及在目的地資料庫中建立的外部資料來源物件。 選取 [產生指令碼] 以 T-SQL 撰寫用來建立外部資料來源的語法指令碼。 選取 [建立] 以建立外部資料來源物件。

![摘要畫面](media/data-virtualization/virtualize-data-summary.png)

如果您選取 [建立]，則會看到目的地資料庫中所建立的外部資料來源物件。

![外部資料來源](media/data-virtualization/external-data-sources.png)

如果您選取 [產生指令碼]，則會看到建立外部資料來源物件所產生的 T-SQL 查詢。

![產生指令碼](media/data-virtualization/generated-script.png)

> [!NOTE]
> [產生指令碼] 應該只顯示在精靈的最後一頁。 目前它會顯示在所有頁面上。

## <a name="next-steps"></a>後續步驟

如需 SQL Server 巨量資料叢集和相關情節的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集](../../big-data-cluster/big-data-cluster-overview.md)。
