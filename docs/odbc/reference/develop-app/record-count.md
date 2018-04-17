---
title: 記錄計數 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af24e83bc4f09f086ab1606dbb6d4dccbd9444e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="record-count"></a>記錄計數
SQL_DESC_COUNT 標頭欄位的描述元是 1 為基底的索引包含資料的最高編號記錄。 此欄位不是所有的資料行或繫結的參數計數。 當配置描述元時，SQL_DESC_COUNT 的初始值為 0。  
  
 驅動程式會採取任何動作的必要配置及維護保存描述元資訊所需的任何儲存體。 應用程式未明確指定的描述元大小不會配置新的記錄。 當應用程式提供其數目高於 SQL_DESC_COUNT 值描述項記錄的資訊時，驅動程式會自動增加 SQL_DESC_COUNT。 當應用程式解除繫結的最高編號的描述項記錄時，驅動程式會自動減少 SQL_DESC_COUNT 包含最高的剩餘繫結記錄的數字。
