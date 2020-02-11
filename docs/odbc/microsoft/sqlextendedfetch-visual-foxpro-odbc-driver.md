---
title: SQLExtendedFetch （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: d58d7885eed1a8ed0611470f29cb24e8072afcb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053797"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級2  
  
 類似于[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ，但會針對每個資料行使用陣列來傳回多個資料列。 如果將資料指標定義為靜態，而不是順向，則結果集會向前復原，而且可以回溯滾動。  
  
 根據預設，Visual FoxPro ODBC 驅動程式不會傳回 FoxPro 資料表中標示為已刪除的資料列。 標記為要刪除但尚未從資料表中移除的資料列不會包含在結果集資料指標中。 您可以使用 [ [SET DELETED](../../odbc/microsoft/set-deleted-command.md) ] 命令來變更此行為。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 。
