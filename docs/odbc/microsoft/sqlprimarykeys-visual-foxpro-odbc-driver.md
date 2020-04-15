---
title: SQL 主鍵(可視化福克斯 Pro ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301543"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:2 級  
  
 返回構成表主鍵的列名稱。 **SQL主要金鑰**的視覺化 FoxPro ODBC 驅動程式實作如下:  
  
-   忽略*szTable 擁有者*與*cbTableOwner 參數*。  
  
-   僅適用於[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的數據源。 如果數據來源是[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄,驅動程式將返回錯誤"驅動程式不支援此函數」。  
  
 有關詳細資訊,請參閱*ODBC 程式者參考*中的[SQL 主要鍵](../../odbc/reference/syntax/sqlprimarykeys-function.md)。
