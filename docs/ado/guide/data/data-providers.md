---
title: 資料提供者 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b49d223faaf5a90a8dcdb6654a9b5107245a9564
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="data-providers"></a>資料提供者
資料提供者會代表不同來源的資料，例如 SQL 資料庫、 編製索引循序性的檔案、 試算表、 文件儲存與郵件檔案。 提供者會公開一致地使用一般的抽象概念，稱為資料列集的資料。  
  
 ADO 是功能強大且靈活，因為它可以連接到數個不同的資料提供者，仍會公開相同的程式設計模型，不論任何給定的提供者的特定功能。 不過，每個資料提供者是唯一的因為您的應用程式搭配 ADO 互動的方式會因資料提供者。  
  
 比方說，用來存取 Microsoft SQL Server 資料庫，SQL Server 的 OLE DB 提供者的功能是大幅不同的 Microsoft OLE DB Provider for Internet Publishing，用來存取檔案在 Web 伺服器上的存放區。
