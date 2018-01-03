---
title: "繫結描述元記錄 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21074ecc6e606b3b235f4eb32bc1f1911136d335
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="bound-descriptor-records"></a>繫結描述元記錄
當應用程式設定 SQL_DESC_DATA_PTR 欄位的描述項記錄，使其不再包含 null 值時，即為記錄*繫結*。  
  
 如果描述元 APD，每個繫結的記錄構成繫結的參數。 輸入參數，應用程式必須繫結參數，以針對每個動態參數標記，在執行陳述式之前的 SQL 陳述式。 輸出參數的應用程式需要繫結參數。  
  
 如果描述元 ARD，描述資料庫資料的資料列，每個繫結的記錄構成繫結的資料行。
