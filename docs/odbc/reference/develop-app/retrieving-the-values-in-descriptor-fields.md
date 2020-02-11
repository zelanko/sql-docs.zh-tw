---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55d7017c659ca4d0b8094ed4a665d27c10b355f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020455"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>擷取描述項欄位中的值
應用程式可以呼叫**SQLGetDescField**來取得描述項記錄的單一欄位。 **SQLGetDescField**可讓應用程式存取 ODBC 中定義的所有描述項欄位，以及驅動程式定義的欄位。  
  
 您可以呼叫**SQLGetDescRec** ，以抓取會影響資料行或參數資料之資料類型和儲存區的多個描述項欄位的設定。
