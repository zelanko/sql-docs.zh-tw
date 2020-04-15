---
title: 分析 ODBC 驅動程式效能
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ed94b29d03fd2b95294bed28201b3bd3b63df45
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281925"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>分析 ODBC 驅動程式效能 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式具有兩個驅動程式特有的選項，可用於分析驅動程式的效能。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式可以在檔中記錄性能統計資訊。 此記錄檔是以 Tab 字元分隔的檔案，可以在 Microsoft Excel 等支援以 Tab 字元分隔之檔案的任何試算表中進行分析。  
  
 此驅動程式也可以記錄長時間執行的查詢 (在指定的時間長度內，沒有從伺服器取得回應的查詢)。 之後，程式設計人員和資料庫管理員就可以分析這些查詢。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [設定檔案驅動程式效能資料&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [&#40;ODBC&#41;记录长时间运行的查询](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 的使用說明主題](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
