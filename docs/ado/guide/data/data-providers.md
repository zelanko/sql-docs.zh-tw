---
description: 資料提供者
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cb448efeb0b78ba6cb29d9acff661308a6bf14bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453580"
---
# <a name="data-providers"></a>資料提供者
資料提供者代表各種不同的資料來源，例如 SQL 資料庫、索引順序檔案、試算表、檔存放區和郵件檔案。 提供者會使用稱為資料列集的通用抽象概念來一致地公開資料。  
  
 ADO 的功能強大且有彈性，因為它可以連接到數個不同的資料提供者，而且仍會公開相同的程式設計模型，而不論任何指定的提供者有哪些特定功能。 不過，因為每個資料提供者都是唯一的，所以您的應用程式與 ADO 互動的方式會因數據提供者而異。  
  
 例如，用來存取 Microsoft SQL Server 資料庫之 SQL Server OLE DB 提供者的功能與功能，與 Microsoft OLE DB Provider for Internet 發行的功能（用來存取 Web 服務器上的檔案存放區）有很大的差別。
