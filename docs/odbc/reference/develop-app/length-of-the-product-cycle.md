---
title: 產品週期的長度 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 203ad92dd6abfc71b0fdeddc466752612e666cee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100448"
---
# <a name="length-of-the-product-cycle"></a>產品週期的長度
有關互通性的最後一個問題是時間。 開發互通的應用程式通常會比開發 noninteroperable 更長的時間。 原因是應用程式必須檢查 DBMS 功能、針對不同的 Dbms 執行相同的工作、解決某些 Dbms 所支援的功能，以及其他操作的方法等等。  
  
 除了開發時間之外，也必須考慮產品存留期。 如果應用程式設計為使用一次，例如在從某個 DBMS 遷移至另一個 DBMS 時傳送資料的應用程式，就沒有必要讓它互通。 應用程式將會使用一次，而且會被捨棄。  
  
 如果應用程式長時間存在，可能會更容易維護為可互通的應用程式。 即使是具有單一 DBMS 做為目標的自訂應用程式也是如此。 原因是可互通的程式碼會使用有限的資料庫功能子集。 驅動程式需要保留這些功能，即使在面對基礎 DBMS 的變更時也一樣。 因此，互通程式碼可以將對 DBMS 所做的變更，轉移到驅動程式開發人員的工作負擔。
