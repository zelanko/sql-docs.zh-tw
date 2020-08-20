---
description: 擷取描述項欄位中的值
title: 正在抓取描述項欄位中的值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494646"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>擷取描述項欄位中的值
應用程式可以呼叫 **SQLGetDescField** 來取得描述項記錄的單一欄位。 **SQLGetDescField** 可讓應用程式存取 ODBC 中定義的所有描述項欄位，以及驅動程式定義的欄位。  
  
 您可以呼叫**SQLGetDescRec**來取出多個描述項欄位的設定，這些描述項欄位會影響資料行或參數資料的資料類型和儲存。
