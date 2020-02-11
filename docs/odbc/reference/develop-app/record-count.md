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
ms.openlocfilehash: d4d684fb6d9614defdca3897c53c4bae9fc231a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138076"
---
# <a name="record-count"></a>記錄計數
描述項的 SQL_DESC_COUNT 標頭欄位是包含資料的最高編號記錄之以一為起始的索引。 這個欄位不是所有系結的資料行或參數的計數。 配置描述項時，SQL_DESC_COUNT 的初始值為0。  
  
 驅動程式會採取任何必要的動作，以配置及維護儲存描述項資訊所需的任何儲存體。 應用程式不會明確指定描述項的大小，也不會配置新的記錄。 當應用程式提供的資訊適用于其數位高於 SQL_DESC_COUNT 值的描述項記錄時，驅動程式會自動增加 SQL_DESC_COUNT。 當應用程式將最高編號的描述項記錄解除系結時，驅動程式會自動減少 SQL_DESC_COUNT，以包含最高剩餘系結記錄的數目。
