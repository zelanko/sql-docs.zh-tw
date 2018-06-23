---
title: 繫結 vs。文字和影像資料行解除繫結 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5129c6b865723721bbb6f176893c950cdf905fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031411"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結 vs。結合的文字和影像資料行
  使用伺服器資料指標， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式已完成最佳化，不傳送未繫結資料**文字**， **ntext**，或**映像**於資料行時間**SQLFetch**會執行。 **文字**， **ntext**，或**映像**不實際擷取資料從伺服器應用程式問題直到[SQLGetData](../native-client-odbc-api/sqlgetdata.md)的資料行。  
  
 可以撰寫許多應用程式，讓沒有**文字**， **ntext**，或**映像**使用者只需向上和向下捲動資料指標中時，會顯示資料。 當使用者選取的資料列，以取得更多詳細資料時，應用程式可以接著呼叫**SQLGetData**擷取**文字**， **ntext**，或**映像**資料。 這將會阻止傳送**文字**， **ntext**，或**映像**資料的任何資料列的使用者未選取，並因此也會阻止傳送非常大大量資料。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](managing-text-and-image-columns.md)   
 [資料指標行為](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  