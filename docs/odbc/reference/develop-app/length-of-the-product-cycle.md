---
title: 在產品週期長度 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a0f319b92afac55101bfe3bca9766a53a91744d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-the-product-cycle"></a>在產品週期的長度
關於互通性的最後一個問題是時間。 通常開發互通的應用程式所花費的時間比開發 noninteroperable 一個。 原因是應用程式必須檢查 DBMS 功能，以不同方式的不同 Dbms 執行相同的工作、 解決某些 Dbms 而非其他電腦所支援的功能和等等。  
  
 除了開發階段，您必須考量產品存留期。 如果應用程式設計成使用一次，例如不同的 dbms 部署移轉到另一個時，將資料傳輸的應用程式沒有任何點進行互通。 應用程式會使用一次，並捨棄。  
  
 如果應用程式將會很長的時間，可能更輕鬆地維護做為互通的應用程式。 這是具有單一的 DBMS 做為目標的自訂應用程式也適用。 原因是互通的程式碼會使用有限的資料庫功能子集。 驅動程式，才能保持可用，而且即使基礎 DBMS 的變更發生這些功能。 因此，具互通性程式碼可以的負擔轉移美術變更至 DBMS 從驅動程式開發人員應用程式開發人員。
