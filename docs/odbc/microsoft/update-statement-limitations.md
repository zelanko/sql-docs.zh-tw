---
description: UPDATE 陳述式限制
title: UPDATE 語句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471397"
---
# <a name="update-statement-limitations"></a>UPDATE 陳述式限制
若要更新資料表的 Paradox 驅動程式，資料表必須有唯一的索引， (Paradox 主鍵) 。 當您使用 Paradox 驅動程式但未執行 Borland 資料庫引擎時，就無法更新 Paradox 資料表。  
  
 文字驅動程式不支援。  
  
 使用 Microsoft Excel 驅動程式時，您可以更新值，但無法從以 Microsoft Excel 試算表為基礎的資料表中刪除資料列。 因此，Microsoft Excel 驅動程式不會將 UPDATE 語句視為正式支援。 只會將 INSERT 語句視為受支援。
