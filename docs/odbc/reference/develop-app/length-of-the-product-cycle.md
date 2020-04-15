---
title: 產品週期的長度 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306191"
---
# <a name="length-of-the-product-cycle"></a>產品週期的長度
關於互操作性的最後一個問題是時間。 開發可互通的應用程式通常比開發不可互通的應用程式需要更長的時間。 原因是應用程式必須檢查 DBMS 功能,針對不同的 DBMS 以不同的方式執行相同的任務,圍繞某些 DBMS 支援的功能(而不是其他 DMS)支援的功能,等等。  
  
 除了開發時間之外,還必須考慮產品生命週期。 如果應用程式設計為一次使用,例如在從一個 DBMS 遷移到另一個 DBMS 時傳輸數據的應用程式,則使其具有互通性是沒有意義的。 該應用程式將使用一次並丟棄。  
  
 如果應用程式將存在很長時間,則作為可互操作的應用程式進行維護可能更容易。 即使以單個 DBMS 為目標的自定義應用程式也是如此。 原因是可互操作的代碼使用有限的資料庫功能子集。 即使面對基礎 DBMS 的更改,也需要驅動程式來保持這些功能可用。 因此,可互操作的代碼可以將應對 DBMS 更改的負擔從應用程式開發人員轉移到驅動程式開發人員。
