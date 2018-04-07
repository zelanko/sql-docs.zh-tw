---
title: 寬 World Importers 文件 |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 99d3bf3913b620a34e284b8277e4c639ba20727a
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2018
---
# <a name="wide-world-importers-documentation"></a>寬 World Importers 文件
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World Importers 是 SQL Server 2016 的新範例資料庫和 Azure SQL Database。 它說明的核心功能的 SQL Server 2016 和 Azure SQL Database，交易處理 (OLTP)、 資料倉儲和分析 (OLAP) 工作負載，以及混合式交易與分析處理 (HTAP) 工作負載。

## <a name="about-this-sample"></a>有關這個範例

Wide World Importers 是完整的資料庫範例同時說明資料庫設計，並說明如何運用 SQL Server 功能，應用程式中。

請注意，此範例旨在代表一般的資料庫。 它不包含 SQL Server 的每一項功能。 資料庫的設計會遵循一組常用的標準，但有許多方法，其中可能會建立一個資料庫。

**最新版本**: [wide world-匯入工具版本](http://go.microsoft.com/fwlink/?LinkID=800630)

**此範例的原始程式碼**:[匯入 world wide 工具](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers)。

**意見反應**： 請將傳送至[ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com)。

此範例的文件的組織方式如下：

## <a name="overview"></a>概觀

概觀範例公司 Wide World Importers，並由此範例工作流程。

## <a name="main-oltp-database-wideworldimporters"></a>主要 OLTP 資料庫 WideWorldImporters

用於交易處理 (OLTP-線上交易處理) 和作業分析 (HTAP-混合式交易式/分析處理) 的 WideWorldImporters 資料庫進行安裝和設定的核心的指示。

結構描述和資料表 WideWorldImporters 資料庫中使用的描述。  

描述如何 WideWorldImporters 運用核心 SQL Server 功能。

WideWorldImporters 資料庫的範例查詢。

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>資料倉儲和分析資料庫 WideWorldImportersDW

指示的安裝和設定 OLAP 資料庫 WideWorldImportersDW。

結構描述和資料表 WideWorldImportersDW 資料庫，也就是資料倉儲和分析處理 (OLAP) 的範例資料庫中使用的描述。

將資料從交易式資料庫 WideWorldImporters 遷移到資料倉儲 WideWorldImportersDW ETL （擷取、 轉換、 載入） 處理序的工作流程。

描述如何 WideWorldImportersDW 運用處理的分析的 SQL Server 功能。

利用 WideWorldImportersDW 資料庫範例分析查詢。

## <a name="data-generation"></a>資料產生

描述如何額外的資料可以在範例資料庫，例如插入銷售產生及購買到目前日期為止的資料。
