---
title: 虛擬化 SQL Server 2019 CTP 2.0 中的外部資料 | Microsoft Docs
description: ''
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dfd4460c51e4aeef8e9faff8479e7edf2678c35f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627316"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>搭配使用資料外部資料表精靈與外部資料表

其中一個 SQL Server 2019 CTP 2.0 重要情節是可以虛擬化資料。  此程序允許將資料保留在其原始位置，但您可以在 SQL Server 執行個體中**虛擬化**資料，以在該處查詢它，如同 SQL Server 中的任何其他資料表。 這會將 ETL 程序的需求降到最低。 這只要使用 Polybase 連接器就能做到。 如需資料虛擬化的詳細資訊，請參閱[開始使用 PolyBase](polybase-guide.md) 文件。

## <a name="launch-the-external-table-wizard"></a>啟動 [外部資料表精靈]

使用在部署指令碼結尾取得的 IP 位址/連接埠號碼 (31433) 來連線至主要執行個體。 展開 [物件總管] 中的 [資料庫] 節點。 然後選取您想要將資料從現有 SQL Server 執行個體虛擬化到其中的其中一個資料庫。 以滑鼠右鍵按一下 [資料庫]，然後從操作功能表中選取 [建立外部資料表]。 這會啟動 [虛擬化資料精靈]。 您也可以鍵入 Ctrl+Shift+P (在 Windows 中) 和 Cmd+Shift+P (在 Mac 中)，以從命令選擇區啟動 [虛擬化資料精靈]。

![虛擬化資料精靈](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>選取資料來源

如果您已從其中一個資料庫啟動此精靈，則可以看到自動填入目的地下拉式清單。 您也可以選擇在此畫面上輸入或變更目的地資料庫。 精靈所支援的外部資料來源類型是 SQL Server 和 Oracle。

> [!NOTE]
>根據預設，會反白顯示 SQL Server


![選取資料來源](media/data-virtualization/select-data-source.png)

按一下 [下一步] 繼續精靈中設定資料庫主要金鑰的下一步。

## <a name="create-database-master-key"></a>建立資料庫主要金鑰

在此步驟中，系統將要求您建立資料庫主要金鑰。 需要建立主要金鑰，因為這會保護外部資料來源所使用的認證。 請選擇主要金鑰的強式密碼。 您也應該使用 BACKUP MASTER KEY 來備份主要金鑰，然後將該備份儲存在安全的離站位置。

![建立資料庫主要金鑰](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 如果您已經有資料庫主要金鑰，則會限制輸入欄位，而且您可能會略過此步驟。您只要按一下 [下一步] 即可繼續前往精靈的下一個頁面。

> [!NOTE]
> 如果您未選擇強式密碼，則精靈將會在最後一個步驟。 這是我們將在即將推出版本中修正使其更具直覺性的已知問題。

## <a name="enter-the-external-data-source-credentials"></a>輸入外部資料來源認證

在此步驟中，請輸入您的外部資料來源和認證詳細資料。 此步驟會建立外部資料來源物件，然後使用認證讓資料庫物件連線至資料來源。 提供外部資料來源的名稱 (例如：Test)，並提供外部資料來源 SQL Server 連線詳細資料：您想要在該伺服器上建立外部資料來源的伺服器名稱和資料庫名稱。

下一步是 [設定認證]，因此請提供認證名稱，這是用來安全地儲存您所建立外部資料來源之登入資訊的資料庫範圍認證名稱 (範例：TestCred)，並提供要連線至資料來源的使用者名稱和密碼。

![外部資料來源認證](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>外部資料表對應

在下一個視窗中，您可以選取想要建立外部檢視的資料表。 選取父資料庫也會包含所有子資料表。 選取資料表時，可以在右側看到對應資料表。 您可以在這裡進行任何「類型」變更，或變更所選取外部資料表本身的名稱。

![外部資料來源認證](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>按兩下另一個選取的資料表將會變更對應檢視。

> [!IMPORTANT]
>外部資料表工具尚未支援相片類型。 建立其中具有相片類型的外部檢視，將會在建立資料表之後擲回錯誤。 不過仍然會建立資料表。

## <a name="summary"></a>摘要

此步驟提供您選項的摘要。 它會提供資料庫範圍認證名稱以及將在目的地資料庫中建立的外部資料來源物件。 在此步驟中，您可以選擇 [產生指令碼] (這會以建立外部資料來源語法的 T-SQL 來撰寫指令碼) 或 [建立] (這會建立外部資料來源物件)。

![摘要畫面](media/data-virtualization/virtualize-data-summary.png)

如果您按一下 [建立]，則可以看到目的地資料庫中所建立的外部資料來源物件。

![外部資料來源](media/data-virtualization/external-data-sources.png)

如果您按一下 [產生指令碼]，則會看到建立外部資料來源物件所產生的 T-SQL 查詢。

![產生指令碼](media/data-virtualization/generated-script.png)

> [!NOTE]
> [產生指令碼] 應該只顯示在精靈的最後一頁。 目前它會顯示在所有頁面中。

## <a name="next-steps"></a>後續步驟

如需 SQL Server 巨量資料叢集和相關情節的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集？](../../big-data-cluster/big-data-cluster-overview.md)。
