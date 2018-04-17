---
title: 資料指標類型 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5b1c041c135586d46f3a777aff411b0e1ed03258
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-types"></a>資料指標類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 定義四種資料指標類型支援的 Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 這些資料指標而能夠偵測結果集的變更，並在資源中使用，例如記憶體及中的空間**tempdb**。 資料指標只有在嘗試重新提取變更過的資料列時，才能偵測到這些資料列的變更；沒有方法可讓資料來源通知資料指標目前所提取的資料列已變更。 交易隔離等級也會影響資料指標偵測到並非透過該資料指標所進行之變更的能力。  
  
 以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援的四種 ODBC 資料指標類型：  
  
-   順向資料指標：此種資料指標不支援捲動，而僅支援從資料指標開頭到結尾循序提取資料列。  
  
-   靜態資料指標內建的**tempdb**開啟資料指標時。 這種資料指標一定會顯示結果集在資料指標開啟時的原貌， 而不會反映出資料的變更。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 靜態資料指標永遠是唯讀的。 因為靜態伺服器資料指標會內建的工作資料表為**tempdb**，資料指標結果集的大小不能超過所允許的最大資料列大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   索引鍵集驅動的資料指標：這種資料指標開啟時，會將結果集中資料列的成員資格和順序設為固定。 您可透過此資料指標看到非索引鍵資料行的變更。  
  
-   動態資料指標是靜態資料指標的相反。 動態資料指標會反映其結果集之中變更的資料列。 每回擷取時結果集之中資料列的資料值、順序和成員均會變動。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
