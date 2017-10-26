---
title: "複製描述 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8cd2ea29713d3bf1e05e76de21397f71dd30c824
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="copying-descriptors"></a>複製的描述元
**SQLCopyDesc**呼叫函式會將一個描述元欄位複製到另一個描述元。 只有應用程式描述項或 IPD，但不是屬於 IRD 欄位複製。 欄位可以從任何類型的描述元複製。 只有在來源和目標的描述元所定義的欄位會複製。 **SQLCopyDesc**不會複製 SQL_DESC_ALLOC_TYPE 欄位中，因為無法變更的描述元的配置類型。 複製的欄位覆寫現有的欄位。  
  
 上一個陳述式控制代碼 ARD 可做為另一個陳述式控制代碼上 APD。 這可讓應用程式來複製資料列，而不複製應用程式層級資料的資料表之間。 若要這樣做，以在 INSERT 陳述式中之參數的參數描述元中重複使用描述擷取的資料列的資料表資料列描述項。 SQL_MAX_CONCURRENT_ACTIVITIES 資訊類型必須是大於 1 的這項作業才能成功。

