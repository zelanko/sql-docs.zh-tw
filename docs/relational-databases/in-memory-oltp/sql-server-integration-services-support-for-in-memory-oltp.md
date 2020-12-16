---
title: 記憶體內部 OLTP 的 SSIS 支援
description: 了解如何在 SQL Server Integration Services 套件中使用原生編譯的預存程序來作為來源與目的地元件。
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f638de7d98cd8e322174172ce918152cbe4623a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485190"
---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>In-Memory OLTP 的 SQL Server Integration Services 支援
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  您可以使用記憶體最佳化資料表、參考記憶體最佳化資料表的檢視，或是原生編譯預存程序作為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 封裝的來源或目的地。 您可以使用 SSIS 封裝的資料流程中的 [ADO NET 來源](../../integration-services/data-flow/ado-net-source.md)、 [OLE DB 來源](../../integration-services/data-flow/ole-db-source.md)或 [ODBC 來源](../../integration-services/data-flow/odbc-source.md) ，並且設定來源元件從記憶體最佳化資料表或檢視擷取資料，或是指定 SQL 陳述式執行原生編譯預存程序。 同樣地，您可以使用 [ADO NET 目的地](../../integration-services/data-flow/ado-net-destination.md)、 [OLE DB 目的地](../../integration-services/data-flow/ole-db-destination.md)或 [ODBC 目的地](../../integration-services/data-flow/odbc-destination.md) 將資料載入記憶體最佳化資料表或檢視，或是指定 SQL 陳述式執行原生編譯預存程序。  
  
 您可以在 SSIS 封裝中設定上述來源和目的地元件從記憶體最佳化資料表和檢視讀取或寫入其中，方式就如同讀寫其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表和檢視。 不過，使用原生編譯預存程序時，需要注意下一節的重點。  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>從 SSIS 封裝叫用原生編譯預存程序  
 若要從 SSIS 套件叫用原生編譯的預存程序，則建議使用 ODBC 來源或 ODBC 目的地，其包含的 SQL 陳述式具有下列格式：不含 **EXEC** 關鍵字的 **\<procedure name>** 。 如果您在 SQL 陳述式中使用 EXEC 關鍵字，則會看見錯誤訊息，因為 ODBC 連接管理員會將 SQL 命令文字解譯為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式而非預存程序，且將使用執行原生編譯的預存程序時不支援的資料指標。 連接管理員會將不含 EXEC 關鍵字的 SQL 陳述式視為預存程序呼叫，而且不會使用資料指標。  
  
 您也可以使用 ADO .NET 來源和 OLE DB 來源叫用原生編譯預存程序，不過我們建議您使用 ODBC 來源。 如果您設定由 ADO .NET 來源執行原生編譯的預存程序，則會看見錯誤訊息，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 的資料提供者 (其為 ADO .NET 來源預設使用) 不支援執行原生編譯的預存程序。 您可以將 ADO .NET 來源設定為使用 ODBC 資料提供者、OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。 不過，請注意，ODBC 來源的執行效能比使用 ODBC 資料提供者的 ADO .NET 來源更佳。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 SQL Server 支援](./transact-sql-support-for-in-memory-oltp.md)  
  
