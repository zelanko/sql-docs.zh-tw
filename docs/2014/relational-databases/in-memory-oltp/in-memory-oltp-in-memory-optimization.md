---
title: 記憶體內部 OLTP (記憶體內部最佳化) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 530e620be1a1c0f9d457eb23712c5228a3883d45
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175916"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>In-Memory OLTP (記憶體中最佳化)

  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]是 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 中的新功能，可大幅提升 OLTP 資料庫應用程式效能。 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 是已整合至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 引擎的記憶體最佳化資料庫引擎，已針對 OLTP 最佳化。

|||
|-|-|
|![Azure 虛擬機器](../../master-data-services/media/azure-virtual-machine.png "Azure 虛擬機器")|您要試用 SQL Server 2016 嗎？ 註冊 Microsoft Azure，然後前往**[這裡](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** 啟動已安裝 SQL Server 2016 的虛擬機器。 當您完成時，可以刪除虛擬機器。|

 若要使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]，您可將經常存取的資料表定義為記憶體最佳化。 記憶體最佳化資料表是可完全交易且持久的，並能利用與以磁碟為基礎的資料表一樣的方式使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 來存取。 查詢可以參考記憶體最佳化資料表和以磁碟為基礎的資料表。 交易可以更新記憶體最佳化資料表和以磁碟為基礎的資料表中的資料。 僅參考記憶體最佳化資料表的預存程序可原生編譯為機器碼，以進一步提升效能。 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎的設計目的是，在衍生自高度向外擴充中間層的 OLTP 類型交易發生極高的工作階段並行處理時使用。 為達成此目的，它使用了不需閂鎖的資料結構，以及開放式、多版本的並行控制。 結果是可針對資料庫交易進行線性比例調整來產生可預期、亞毫秒低延遲及高輸送量。 實際效能獲益取決於許多因素，但通常可以獲得 5 到 20 倍的效能提升。

 下表摘要說明使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]時可能獲益最多的工作負載模式：

|實作案例|實作案例|[!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 的優點|
|-----------------------------|-----------------------------|-------------------------------------|
|來自多個並行連接的高度資料插入比率。|主要的附加專用存放區。<br /><br /> 跟不上插入工作負載。|排除競爭。<br /><br /> 減少記錄。|
|定期批次插入和更新的讀取效能與比例調整。|高效能讀取作業，特別是在每個伺服器要求都有數個讀取作業要執行時。<br /><br /> 無法符合相應增加的要求。|在新資料到達時排除競爭。<br /><br /> 較低延遲的資料擷取。<br /><br /> 將程式碼執行時間縮到最短。|
|資料庫伺服器中密集的商務邏輯處理。|插入、更新及刪除工作負載。<br /><br /> 預存程序內部的大量計算。<br /><br /> 讀寫競爭。|排除競爭。<br /><br /> 將程式碼執行時間縮到最短，以減少延遲並提高輸送量。|
|低度延遲。|要求一般資料庫解決方案無法達成的低度延遲商務交易。|排除競爭。<br /><br /> 將程式碼執行時間縮到最短。<br /><br /> 低度延遲的程式碼執行。<br /><br /> 有效率的資料擷取。|
|工作階段狀態管理。|經常性插入、更新及點查閱。<br /><br /> 從許多無狀態的 Web 伺服器大範圍載入。|排除競爭。<br /><br /> 有效率的資料擷取。<br /><br /> 使用非持久性的資料表時，選擇性地減少或移除 IO|

 如需[!INCLUDE[hek_2](../../../includes/hek-2-md.md)]將產生最佳效能提升之案例的詳細資訊，請參閱[記憶體內部 OLTP-一般工作負載模式和遷移考慮](https://msdn.microsoft.com/library/dn673538.aspx)。

 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 對於執行短期交易的 OLTP 效能改善效果最好。

 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 將提升的效能模式包含並行案例、點查閱、含有大量執行插入和更新的工作負載，以及預存程序中的商務邏輯。

 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的整合意味著記憶體最佳化資料表和磁碟資料表可並存於相同的資料庫中，而且您將能跨這兩類資料表進行查詢。

 在 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 中， [!INCLUDE[tsql](../../../includes/tsql-md.md)] 對於 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]介面區的支援有一些限制。

 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 透過使用下列項目達到顯著的效能和延展性提升：

-   為存取記憶體駐留的資料最佳化的演算法。

-   消除邏輯鎖定的開放式並行存取控制。

-   不需鎖定的物件，可消除所有實體的鎖定與閂鎖。 執行交易式工作的執行緒不會使用鎖定或閂鎖來進行並行存取控制。

-   原生編譯的預存程序，在存取記憶體最佳化資料表時，其效能明顯優於解譯的預存程序。

> [!IMPORTANT]
>  您需要在資料表和預存程序中進行一些語法變更，才能使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]。 如需詳細資訊，請參閱[移轉至記憶體內部 OLTP](migrating-to-in-memory-oltp.md)。 在您嘗試將磁碟資料表移轉至記憶體最佳化資料表之前，請先閱讀[判斷是否應將資料表或預存程序匯出至記憶體內部 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)查看哪些資料表和預存程序將可獲益於 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]。

## <a name="in-this-section"></a>本節內容
 本節提供下列概念的相關資訊：

|主題|描述|
|-----------|-----------------|
|[使用記憶體最佳化資料表的需求](memory-optimized-tables.md)|討論有關使用記憶體最佳化資料表的硬體和軟體需求以及方針。|
|[在 VM 環境使用記憶體中的 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|涵蓋在虛擬化環境中使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 。|
|[記憶體內部 OLTP 程式碼範例](in-memory-oltp-code-samples.md)|包含程式碼範例，示範如何建立及使用記憶體最佳化資料表。|
|[記憶體優化資料表](memory-optimized-tables.md)|介紹記憶體最佳化的資料表。|
|[記憶體優化資料表變數](../../database-engine/memory-optimized-table-variables.md)|程式碼範例，示範如何使用記憶體最佳化的資料表變數取代傳統資料表變數，以減少 tempdb 的使用量。|
|[記憶體最佳化資料表上的索引](../../database-engine/indexes-on-memory-optimized-tables.md)|介紹記憶體最佳化索引。|
|[原生編譯的預存程式](natively-compiled-stored-procedures.md)|介紹原生編譯的預存程序。|
|[為記憶體中的 OLTP 管理記憶體](../../database-engine/managing-memory-for-in-memory-oltp.md)|了解及管理系統上的記憶體使用量。|
|[建立及管理記憶體最佳化物件的儲存體](creating-and-managing-storage-for-memory-optimized-objects.md)|討論資料與差異檔案 (儲存記憶體最佳化之資料表中的交易資訊)。|
|[備份、還原及復原記憶體最佳化資料表](restore-and-recovery-of-memory-optimized-tables.md)|討論記憶體最佳化資料表的備份、還原及復原。|
|[記憶體中 OLTP 的 Transact-SQL 支援](transact-sql-support-for-in-memory-oltp.md)|討論適用於 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 的 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]支援。|
|[記憶體內部 OLTP 資料庫的高可用性支援](high-availability-support-for-in-memory-oltp-databases.md)|討論可用性群組與 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]中的容錯移轉叢集。|
|[記憶體中 OLTP 的 SQL Server 支援](sql-server-support-for-in-memory-oltp.md)|列出為支援記憶體最佳化資料表新增和更新的語法和功能。|
|[移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)|討論如何將以磁碟為基礎的資料表移轉到記憶體最佳化的資料表。|

 有關 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 的詳細資訊可於下列位置取得：

-   [Microsoft？SQL Server？？2014產品指南](https://www.microsoft.com/download/confirmation.aspx?id=39269)

-   [In-Memory OLTP 部落格](https://go.microsoft.com/fwlink/?LinkId=311696)

-   [記憶體內部 OLTP-一般工作負載模式和遷移考慮](https://msdn.microsoft.com/library/dn673538.aspx)

-   [SQL Server In-Memory OLTP 內部概觀](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
    <!--
         (https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
         (/sql/relational-databases/in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016?view=sql-server-2016)
    -->

## <a name="see-also"></a>另請參閱
 [資料庫功能](../database-features.md)


