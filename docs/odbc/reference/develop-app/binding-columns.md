---
description: 繫結資料行
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
ms.openlocfilehash: 8f3f02ec6487b34a6ca2c973c3115c3940ca8fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429430"
---
# <a name="binding-columns"></a>繫結資料行
從資料來源提取的資料會在應用程式已針對此用途配置的變數中傳回給應用程式。 在這麼做之前，應用程式必須將這些變數與結果集的資料行產生 *關聯或系*結;就概念而言，此程式與將應用程式變數系結至語句參數的程式相同。 當應用程式將變數系結至結果集資料行時，它會描述該驅動程式的變數位址、資料類型等等。 驅動程式會將這項資訊儲存在它針對該語句所維護的結構中，並在提取資料列時使用該資訊來傳回資料行中的值。  
  
 此章節包含下列主題。  
  
-   [繫結結果集資料行](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
