---
title: 繫結描述項記錄 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d0016a2849feb5656cb3cd6dd46eff444f37058
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118755"
---
# <a name="bound-descriptor-records"></a>繫結描述項記錄
當應用程式設定 SQL_DESC_DATA_PTR 欄位的描述項記錄，使其不再包含 null 值時，即為資料錄*繫結*。  
  
 如果描述元 APD，每個繫結的資料錄會構成繫結的參數。 輸入參數，應用程式必須繫結參數，以針對每個動態參數標記，在執行陳述式之前的 SQL 陳述式中。 輸出參數的應用程式需要繫結參數。  
  
 如果描述元 ARD，描述資料庫資料的資料列，每個繫結的資料錄會構成繫結的資料行。
