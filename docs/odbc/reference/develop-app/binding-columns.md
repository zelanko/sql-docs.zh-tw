---
title: 系結資料行 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301819"
---
# <a name="binding-columns"></a>繫結資料行
從資料來源提取的資料會以應用程式已配置給此用途的變數傳回給應用程式。 在完成這項作業之前，應用程式必須將這些變數與結果集的資料行建立*關聯或系*結;就概念而言，這個程式與將應用程式變數系結至語句參數相同。 當應用程式將變數系結至結果集資料行時，它會描述該驅動程式的變數位址、資料類型等等。 驅動程式會將這項資訊儲存在它為該語句維護的結構中，並在提取資料列時，使用此資訊來傳回資料行中的值。  
  
 此章節包含下列主題。  
  
-   [繫結結果集資料行](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
