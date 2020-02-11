---
title: SQLSpecialColumns （Visual FoxPro ODBC Driver） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b690cceecb6c9980f5d84e96bccb1b02f014c026
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093090"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 抓取可唯一識別資料表中之資料列的最佳資料行集合。  
  
 Visual FoxPro ODBC 驅動程式會傳回在 FoxPro 資料表上組成主鍵的資料行。 （請參閱[SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)）。如果使用設定為 SQL_ROWVER 的*fColType*來呼叫，則不會傳回任何資料行。 **SQLSpecialColumns**僅適用于[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 。
