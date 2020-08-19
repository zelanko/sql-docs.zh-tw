---
description: 繫結描述項記錄
title: 系結描述項記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcf88374967b5a9d8426d16c9e92c06e4eef32cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476800"
---
# <a name="bound-descriptor-records"></a>繫結描述項記錄
當應用程式設定描述項記錄的 SQL_DESC_DATA_PTR 欄位，使其不再包含 null 值時， *就會將*記錄視為已系結。  
  
 如果描述元是 APD，則每個系結記錄都會構成系結參數。 針對輸入參數，應用程式必須在執行語句之前，先系結 SQL 語句中每個動態參數標記的參數。 針對輸出參數，應用程式不需要系結參數。  
  
 如果描述項是描述資料庫資料列的 ARD，則每個系結記錄都會構成一個系結資料行。
