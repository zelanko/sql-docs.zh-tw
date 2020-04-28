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
ms.openlocfilehash: 40506ec971782c5e9108a34fd240faabcc2756b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925650"
---
# <a name="data-providers"></a>資料提供者
資料提供者代表各種不同的資料來源，例如 SQL 資料庫、索引順序檔案、試算表、檔存放區和郵件檔案。 提供者會使用稱為資料列集的通用抽象概念來一致地公開資料。  
  
 ADO 的功能強大且有彈性，因為它可以連接到數種不同的資料提供者，而且仍然會公開相同的程式設計模型，不論任何指定的提供者的特定功能為何。 不過，因為每個資料提供者都是唯一的，所以您的應用程式與 ADO 互動的方式會因數據提供者而異。  
  
 例如，SQL Server 的 OLE DB 提供者的功能和功能（用來存取 Microsoft SQL Server 資料庫）與用來存取 Web 服務器上檔案存放區的 Microsoft OLE DB 提供者（用於網際網路發行）不同。
