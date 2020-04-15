---
title: 繫結欄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301819"
---
# <a name="binding-columns"></a>繫結資料行
從數據源獲取的數據以應用程式為此分配的變數返回到應用程式。 在此操作之前,應用程式必須將這些變數關聯或綁定到結果集的列;否則,應用程式必須將這些變數關聯或*綁定*到結果集的列中。從概念上講,此過程與綁定應用程式變數到語句參數相同。 當應用程式將變數綁定到結果集列時,它將該變數 (位址、數據類型等) 描述給驅動程式。 驅動程式將此資訊存儲在它為該語句維護的結構中,並使用該資訊在提取行時從列返回值。  
  
 此章節包含下列主題。  
  
-   [繫結結果集資料行](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
