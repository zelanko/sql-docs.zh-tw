---
description: SQLExtendedFetch (Visual FoxPro ODBC Driver)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f938dda4e9e474854d62c50401ee0bf91317983
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449170"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級2  
  
 類似于 [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ，但會使用每個資料行的陣列傳回多個資料列。 結果集是向前滾動的，如果資料指標定義為靜態（而非順向），就可以將它設為可回溯滾動。  
  
 根據預設，Visual FoxPro ODBC 驅動程式不會傳回在 FoxPro 資料表中標示為已刪除的資料列。 結果集資料指標中不包含標示為要刪除但尚未從資料表中移除的資料列。 您可以使用 [ [設定已刪除](../../odbc/microsoft/set-deleted-command.md) ] 命令來變更此行為。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 。
