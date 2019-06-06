---
title: 資料提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 30d1e1515ed3e84640fe1ca004cb7cbf4383ce97
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718722"
---
# <a name="data-providers"></a>資料提供者
資料提供者會代表不同來源的資料，例如 SQL 資料庫、 編製索引-循序檔案、 試算表、 文件存放區和郵件檔。 提供者會公開一致地使用常見的抽象概念，稱為資料列集的資料。  
  
 ADO 是功能強大且靈活的因為它可以連線到任何數個不同的資料提供者，並仍會公開相同的程式設計模型，不論任何指定的提供者的特定功能。 不過，因為每個資料提供者是唯一的您的應用程式與 ADO 之間的互動方式會因資料提供者。  
  
 比方說，功能的 OLE DB Provider for SQL Server，用來存取 Microsoft SQL Server 資料庫，是相當不同的 Microsoft OLE DB Provider for Internet Publishing，用來存取檔案在 Web 伺服器上的存放區。
