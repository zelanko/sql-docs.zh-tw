---
description: SQLSpecialColumns (Visual FoxPro ODBC Driver)
title: SQLSpecialColumns (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e83568c8370b56decb7c3f7c90cda443b88a72a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421602"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 抓取可在資料表中唯一識別資料列的最佳資料行集合。  
  
 Visual FoxPro ODBC 驅動程式會傳回組成 FoxPro 資料表之主鍵的資料行。  (請參閱 [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。 ) 如果是以設定為 SQL_ROWVER 的 *fColType* 呼叫，則不會傳回任何資料行。 **SQLSpecialColumns** 僅適用于 [資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 。
