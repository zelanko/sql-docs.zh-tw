---
title: 分析 ODBC 驅動程式效能的使用說明主題（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 782558d3c8325f1886310fea4d0291982544d16c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73791040"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>分析 ODBC 驅動程式效能 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式具有兩個驅動程式特有的選項，可用於分析驅動程式的效能。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式可以將效能統計資料記錄在檔案中。 此記錄檔是以 Tab 字元分隔的檔案，可以在 Microsoft Excel 等支援以 Tab 字元分隔之檔案的任何試算表中進行分析。  
  
 此驅動程式也可以記錄長時間執行的查詢 (在指定的時間長度內，沒有從伺服器取得回應的查詢)。 之後，程式設計人員和資料庫管理員就可以分析這些查詢。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [分析驅動程式效能&#40;資料 ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [記錄長時間執行的&#40;查詢 ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 的使用說明主題](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
