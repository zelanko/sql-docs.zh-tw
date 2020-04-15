---
title: SQLTransact(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299218"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 請求所有與連接關聯的語句句柄 *(hstmt*s) 或與環境句柄關聯的所有連接*henv*的所有活動操作的提交或回滾操作。 **SQLTransact**僅適用於[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的數據源。  
  
 如果在手動模式下提交失敗,則事務將保持活動狀態;如果提交處於手動模式下,則事務將保持活動狀態。您可以選擇回滾事務或重試提交操作。 如果在自動事務模式下提交操作失敗,則事務將自動回滾;事務不能處於非活動狀態。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLTransact。](../../odbc/reference/syntax/sqltransact-function.md)
