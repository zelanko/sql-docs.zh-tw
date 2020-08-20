---
description: SQLTransact (Visual FoxPro ODBC Driver)
title: SQLTransact (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1deed379c456ba2f15d30b6783c95d657e688457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500111"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 針對所有語句控制碼上所有使用中的作業要求認可或回復作業， (*hstmt*s) 與連接相關聯，或與環境控制碼 *henv*相關聯的所有連接。 **SQLTransact** 僅適用于 [資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。  
  
 如果在手動模式下認可失敗，則交易會維持作用中狀態;您可以選擇回復交易或重試認可作業。 如果在自動交易模式下認可作業失敗，則會自動回復交易;交易不能為非使用中。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) 。
