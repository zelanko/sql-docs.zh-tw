---
title: 繫結與Text 和 Image 資料行解除繫結 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf8ac0cf868394d9aa8063220939feee69ac2f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626581"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結與未繫結的 Text 和 Image 資料行
  使用伺服器資料指標，當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式已最佳化，不傳送未繫結資料**文字**， **ntext**，或**映像**於資料行時間**SQLFetch**會執行。 **文字**， **ntext**，或**映像**不會實際擷取資料從伺服器應用程式問題直到[SQLGetData](../native-client-odbc-api/sqlgetdata.md)的資料行。  
  
 可以撰寫許多應用程式，讓沒有**文字**， **ntext**，或**映像**使用者只要向上和向下捲動資料指標中時，會顯示資料。 當使用者選取的資料列，以取得詳細資料時，應用程式可以接著呼叫**SQLGetData**來擷取**文字**， **ntext**，或**映像**資料。 這將會阻止傳送**文字**， **ntext**，或**映像**資料的任何資料列的使用者未選取，並因此可以阻止傳送非常大大量的資料。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](managing-text-and-image-columns.md)   
 [資料指標行為](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
