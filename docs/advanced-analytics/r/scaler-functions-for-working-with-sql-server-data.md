---
title: 使用 SQL Server 資料 RevoScaleR 函數 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d97a75cdc7da6a05847373b259ef562353d578ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203490"
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>使用 SQL Server 資料 RevoScaleR 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題提供適用於使用 SQL Server 資料 RevoScaleR 中提供的主要函數的概觀。

ScaleR 函數和使用方式的完整清單，請參閱[Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)參考。

## <a name="create-sql-server-data-sources"></a>建立 SQL Server 資料來源

下列函數可讓您定義 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料來源。 資料來源物件是可一起指定連接字串和您想要之資料集 (可定義為資料表、檢視或查詢) 的容器。 不支援預存程序呼叫。

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -定義[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料來源物件。

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -建立其他的 ODBC 資料庫的資料物件。 

## <a name="perform-ddl-statements"></a>執行 DDL 陳述式

如果您有執行個體和資料庫的必要權限，您可以從 R 執行 DDL 陳述式。 下列函數會使用 ODBC 呼叫來執行 DDL 陳述式，或擷取資料庫結構描述。

+ `rxSqlServerTableExists` 和[rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -卸除[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料表，或檢查資料庫資料表或物件存在

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -執行資料定義語言 (DDL) 命令定義，或操作資料庫物件。 此函數無法傳回資料，並只會用於擷取或修改物件結構描述或中繼資料。

## <a name="define-or-manage-compute-contexts"></a>定義或管理的計算內容

下列函數可讓您定義新的計算內容、切換計算內容，或識別目前的計算內容。

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext)：建立計算內容。

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)：產生 SQL Server 計算內容，該計算內容可讓 **ScaleR** 函數在 SQL Server R Services 中執行。 此計算內容目前只支援 Windows 上的 SQL Server 執行個體。

+ `rxGetComputeContext` 和[rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) -取得或設定作用中的計算內容。

## <a name="move-data-and-transform-data"></a>移動資料和轉換資料

建立資料來源物件之後，您可以使用物件資料載入、 轉換資料，或將新資料寫入至指定的目的地。 根據來源中的資料大小，您也可以定義資料來源中的批次大小，以及以區塊移動資料。

+ [rxOpen 方法](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods)-請檢查資料來源是否可用，開啟或關閉資料來源、 從來源讀取資料、 寫入資料至目標，並關閉資料來源

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -進入檔案儲存體或資料框架，從資料來源移動資料。

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -轉換同時移動資料來源之間的資料。

下列函數可以用來建立 XDF 格式的本機資料存放區。 當使用的資料超過可從資料庫以單一批次傳送的資料，或是超過記憶體內可容納的資料時，這個檔案非常實用。

比方說，如果定期在資料庫的本機工作站之間移動大量資料，而不是查詢資料庫中重複的每個 R 作業，您可以使用 XDF 檔案做為一種快取儲存在本機的資料，然後在您的 R 工作區中使用它。

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -建立 XDF 資料物件

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -XDF 檔案中的資料讀入資料框架

如需有關使用這些函式的詳細資訊，包括使用資料來源而不是[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，請參閱[如何引導資料分析 Microsoft R](https://docs.microsoft.com/r-server/r/how-to-introduction)。
