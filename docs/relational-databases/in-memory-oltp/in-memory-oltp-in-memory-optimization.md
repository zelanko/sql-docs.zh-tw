---
title: "記憶體內部 OLTP (記憶體內部最佳化) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/22/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
caps.latest.revision: 106
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b377f0c359751a5c970ceef2e1d7fa6bc556e3d7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="in-memory-oltp-in-memory-optimization"></a>In-Memory OLTP (記憶體中最佳化)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 可大幅提升交易處理、資料擷取和資料載入，以及暫時性資料案例的效能。  若要跳至快速測試您自己的記憶體最佳化資料表和原生編譯預存程序所需的基本程式碼和知識，請參閱
 -  [快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)。  
 
一段 17 分鐘的影片，可說明記憶體內部 OLTP 並示範效能優點：

-  [SQL Server 2016 中的記憶體內部 OLTP](https://www.youtube.com/watch?v=l5l5eophmK4)。

下載影片中所使用之記憶體內部 OLTP 的效能示範： 

- [記憶體內部 OLTP 效能示範 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

如需記憶體內部 OLTP 的更詳細概觀，以及檢閱案例以查看來自此技術的效能效益：

- [概觀和使用案例](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 請注意， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術，可改善交易處理的效能。 如需改善報告和分析查詢效能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術，請參閱 [資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)。
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]中的記憶體內部 OLTP 進行了幾項改進。 已增加 Transact-SQL 介面區，讓移轉資料庫應用程式更容易。 已新增對記憶體最佳化資料表和原生編譯預存程序的執行 ALTER 作業支援，讓維護應用程式更容易。 如需 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 中新功能的資訊，請參閱[資料行存放區索引 - 新功能](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)。  
  
> [!NOTE]  
>  **現在就試試看**  
>   
>  記憶體內部 OLTP 適用於 Premium Azure SQL Database 中。 若要開始使用記憶體內部 OLTP 以及 Azure SQL Database 中的資料行存放區，請參閱 [在 SQL Database 中使用記憶體內部技術最佳化效能](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)。  
  

## <a name="in-this-section"></a>本節內容  
 本節包含下列主題：  
  
|主題|Description|  
|-----------|-----------------|  
|[快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|適當探討記憶體內部 OLTP|
|[概觀和使用案例](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|記憶體內部 OLTP 是什麼，以及有哪些效能案例可看到效能效益的概觀。|
|[使用記憶體最佳化資料表的需求](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|討論有關使用記憶體最佳化資料表的硬體和軟體需求以及方針。|  
|[記憶體內部 OLTP 程式碼範例](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|包含程式碼範例，示範如何建立及使用記憶體最佳化資料表。|  
|[記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|介紹記憶體最佳化的資料表。|  
|[記憶體最佳化資料表變數](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|程式碼範例，示範如何使用記憶體最佳化的資料表變數取代傳統資料表變數，以減少 tempdb 的使用量。|  
|[記憶體最佳化資料表上的索引](http://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|介紹記憶體最佳化索引。|  
|[原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|介紹原生編譯的預存程序。|  
|[為記憶體內部 OLTP 管理記憶體](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|了解及管理系統上的記憶體使用量。|  
|[建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|討論資料與差異檔案 (儲存記憶體最佳化之資料表中的交易資訊)。|  
|[備份、還原及復原記憶體最佳化資料表](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|討論記憶體最佳化資料表的備份、還原及復原。|  
|[記憶體內部 OLTP 的 Transact-SQL 支援](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|討論適用於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]支援。|  
|[記憶體內部 OLTP 資料庫的高可用性支援](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|討論可用性群組與 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]中的容錯移轉叢集。|  
|[記憶體內部 OLTP 的 SQL Server 支援](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|列出為支援記憶體最佳化資料表新增和更新的語法和功能。|  
|[移轉至記憶體內部 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|討論如何將以磁碟為基礎的資料表移轉到記憶體最佳化的資料表。|  
  
 有關 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 的詳細資訊可於下列位置取得：  

- [說明記憶體內部 OLTP 並示範其效能優點的影片](https://www.youtube.com/watch?v=l5l5eophmK4)。

- [記憶體內部 OLTP 效能示範 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server 記憶體內部 OLTP 內部技術白皮書](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [SQL Server 記憶體內部 OLTP 和資料行存放區功能的比較](http://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   SQL Server 2016 中記憶體內部 OLTP 的新功能 [第 1 部分](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) 和 [第 2 部分](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [記憶體內部 OLTP - 一般工作負載模式和移轉考量](http://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [記憶體內部 OLTP 部落格](http://go.microsoft.com/fwlink/?LinkId=311696)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫功能](../../relational-databases/database-features.md)  
  
  

