---
title: 在產品週期的長度 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100448"
---
# <a name="length-of-the-product-cycle"></a>產品週期的長度
關於互通性的最後一個問題是時間。 通常開發的可互通的應用程式所花費的時間比開發 noninteroperable 一個。 原因是應用程式必須檢查 DBMS 功能，以不同的方式執行相同的工作，針對不同的 Dbms、 解決由某些 Dbms 而非其他支援的功能和等等。  
  
 除了開發階段，必須視為產品的壽命期間。 如果應用程式設計來一次，例如不同的 dbms 部署移轉到另一個時，將資料傳輸的應用程式沒有任何點進行互通。 應用程式會使用一次，並捨棄。  
  
 如果應用程式將會有很長的時間，可能更輕鬆地維護可互通的應用程式。 這是也適用於具有單一的 DBMS，做為目標的自訂應用程式。 原因是互通的程式碼會使用資料庫功能的有限的子集。 驅動程式，才能讓這些功能可供使用，即使基礎 DBMS 的變更。 因此，具互通性的程式碼可以的負擔轉移如何因應的變更對 DBMS 從驅動程式開發人員應用程式開發人員。
