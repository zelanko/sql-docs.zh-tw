---
description: 產品週期的長度
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1484079a09d10864e0563db95208e926a959d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476580"
---
# <a name="length-of-the-product-cycle"></a>產品週期的長度
互通性的最後一個問題是時間。 開發互通的應用程式通常比開發 noninteroperable 的應用程式需要更長的時間。 原因是，應用程式必須檢查 DBMS 功能、針對不同 Dbms 執行相同的工作、解決某些 Dbms （而非其他 Dbms）所支援的功能等等。  
  
 除了開發時間之外，還必須考慮產品存留期。 如果應用程式設計為使用一次，例如將資料從某個 DBMS 遷移到另一個 DBMS 時傳送資料的應用程式，則不會讓它互通。 應用程式將會使用一次並捨棄。  
  
 如果應用程式有很長一段時間，就可以更容易維護為可互通的應用程式。 即使是以單一 DBMS 做為目標的自訂應用程式，也是如此。 原因是可互通的程式碼會使用有限的資料庫功能子集。 即使在面對基礎 DBMS 的變更時，還是需要驅動程式才能保持這些功能的可用。 因此，互通的程式碼可能會將從應用程式開發人員變更至 DBMS 的負擔轉移至驅動程式開發人員。
