---
description: 多個 hstmt (Paradox 驅動程式)
title: 多個 hstmt (Paradox 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687b87f07142ad23f6faf7155ae974a6d93deab4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449400"
---
# <a name="multiple-hstmts-paradox-driver"></a>多個 hstmt (Paradox 驅動程式)
使用 ODBC Paradox 驅動程式時，如果您想要使用多個 *hstmt* 在資料表上執行查詢，則資料表必須有唯一的索引， (Paradox primary key) 。
