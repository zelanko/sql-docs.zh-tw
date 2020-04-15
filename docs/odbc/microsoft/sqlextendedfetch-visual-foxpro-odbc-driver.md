---
title: SQL 擴展取得(可視化福克斯 Pro ODBC 驅動程式) |微軟文件
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
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298648"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:2 級  
  
 與[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)類似,但使用每個列的陣列返回多行。 結果集是可向前滾動的,如果游標定義為靜態的,而不是僅向前滾動,則可以向後滾動。  
  
 預設情況下,Visual FoxPro ODBC 驅動程式不會返回在 FoxPro 表中標記為已刪除的行。 標記為刪除但尚未從表中刪除的行不包括在結果集游標中。 您可以使用[SET DELETED](../../odbc/microsoft/set-deleted-command.md)命令更改此行為。  
  
 有關詳細資訊,請參閱*ODBC 程式者參考*中的[SQL 擴充取得](../../odbc/reference/syntax/sqlextendedfetch-function.md)。
