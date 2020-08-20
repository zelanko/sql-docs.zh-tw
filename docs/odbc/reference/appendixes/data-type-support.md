---
description: 資料類型支援
title: 資料類型支援 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ab0fd163713a7f6657d8ce446336f5c35a3dd00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456635"
---
# <a name="data-type-support"></a>資料類型支援
ODBC 驅動程式至少必須支援 SQL_CHAR 和 SQL_VARCHAR 的其中一個。 其他資料類型的支援是由驅動程式或資料來源的 SQL-92 一致性層級所決定。 應用程式應該呼叫 **SQLGetTypeInfo** 來判斷驅動程式所支援的資料類型。  
  
 如需資料類型的詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
