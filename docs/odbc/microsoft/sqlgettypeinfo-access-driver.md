---
title: SQLGetTypeInfo(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddfa9bd29f0834adf1c211f9b8a111db0b94d3fe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295148"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLGetTypeInfo**生成的表中返回的類型(TYPE_NAME)的名稱將是數據源最常用的名稱。  
  
 SQL_ALL_EXCEPT_LIKE將在位元組、計數器、雙、單、長和短資料類型的 SEARCHABLE 列中返回。 (可以通過使用 ODBC 規範轉換函數將值轉換為字元,然後執行比較來實現 LIKE 功能。
