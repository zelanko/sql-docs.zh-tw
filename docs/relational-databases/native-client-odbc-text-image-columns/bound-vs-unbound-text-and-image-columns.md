---
title: "繫結 vs。文字和影像資料行解除繫結 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e511e9861b851f08080752f1d85b75c8887db5df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結 vs。結合的文字和影像資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用伺服器資料指標， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式已完成最佳化，不傳送未繫結資料**文字**， **ntext**，或**映像**當時的資料行**SQLFetch**會執行。 **文字**， **ntext**，或**映像**不實際擷取資料從伺服器應用程式問題直到[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)資料行。  
  
 可以撰寫許多應用程式，讓沒有**文字**， **ntext**，或**映像**使用者只需向上和向下捲動資料指標中時，會顯示資料。 當使用者選取的資料列，以取得更多詳細資料時，應用程式可以接著呼叫**SQLGetData**擷取**文字**， **ntext**，或**映像**資料。 這將會阻止傳送**文字**， **ntext**，或**映像**資料的任何資料列的使用者未選取，並因此也會阻止傳送非常大量的資料。  
  
## <a name="see-also"></a>請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
