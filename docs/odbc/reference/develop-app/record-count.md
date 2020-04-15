---
title: 記錄計數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281814"
---
# <a name="record-count"></a>記錄計數
描述符的SQL_DESC_COUNT標頭欄位是包含數據的最高編號記錄的基於一個索引。 此欄位不是綁定的所有列或參數的計數。 分配描述符時,SQL_DESC_COUNT的初始值為 0。  
  
 驅動程式執行任何必要的操作來分配和維護它保存描述符資訊所需的任何存儲。 應用程式不顯式指定描述符的大小,也不會分配新記錄。 當應用程式為數位高於SQL_DESC_COUNT值的描述符記錄提供資訊時,驅動程式會自動增加SQL_DESC_COUNT。 當應用程式取消綁定編號最高的描述符記錄時,驅動程式會自動減少SQL_DESC_COUNT以包含剩餘綁定記錄的最高數。
