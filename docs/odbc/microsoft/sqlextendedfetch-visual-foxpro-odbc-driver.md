---
title: SQLExtendedFetch (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2d01c25044bf7b03e2fabe9c615668fc7837312
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313244"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 2  
  
 類似於[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)但會傳回每個資料行使用陣列的多個資料列。 結果集是順向可捲動，並可回溯可捲動資料指標會定義為靜態，不順如果。  
  
 根據預設，Visual FoxPro ODBC 驅動程式不會傳回標記為 FoxPro 資料表中刪除資料列。 標示為刪除但尚未從資料表移除資料列不會納入結果集資料指標。 您可以使用來變更此行為[設定刪除](../../odbc/microsoft/set-deleted-command.md)命令。  
  
 如需詳細資訊，請參閱 < [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)中*ODBC 程式設計人員參考*。
