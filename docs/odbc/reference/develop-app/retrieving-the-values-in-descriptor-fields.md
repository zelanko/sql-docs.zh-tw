---
title: 擷取描述項欄位中的值 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020455"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>擷取描述項欄位中的值
應用程式可以呼叫**SQLGetDescField**取得的單一欄位的描述項記錄。 **SQLGetDescField**在 ODBC 中，定義的所有描述項欄位和驅動程式定義欄位也會提供應用程式存取權。  
  
 **SQLGetDescRec**可以呼叫以擷取多個會影響資料類型的描述項欄位的設定和資料行或參數資料的儲存體。
