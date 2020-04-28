---
title: SQLTransact （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 3910f24578bcbc409a84573e994c0680ed5949b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299218"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 針對與連接相關聯之所有語句控制碼（*hstmt*s）上的所有作用中作業，或與該環境控制碼*henv*相關聯的所有連接，要求認可或回復操作。 **SQLTransact**僅適用于[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。  
  
 如果在手動模式下認可失敗，則交易會保持作用中狀態;您可以選擇復原交易，或重試認可作業。 如果在自動交易模式中，認可作業失敗，則會自動回復交易。交易不可為非使用中。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) 。
