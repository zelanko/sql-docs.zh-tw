---
title: 記錄計數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610421"
---
# <a name="record-count"></a>記錄計數
SQL_DESC_COUNT 標頭欄位，描述元是以一為基的索引包含資料的最高編號記錄。 此欄位不是所有的資料行或參數繫結的計數。 當配置描述元時，SQL_DESC_COUNT 的初始值為 0。  
  
 驅動程式會採取任何動作的必要配置及維護保存描述元資訊所需的儲存體。 應用程式未明確指定的描述項的大小不配置新的記錄。 當應用程式提供其編號大於 SQL_DESC_COUNT 值描述項記錄的資訊時，驅動程式會自動增加 SQL_DESC_COUNT。 當應用程式解除繫結的最高編號的描述項記錄時，驅動程式會自動減少 SQL_DESC_COUNT 最高其餘的繫結資料錄數目。
