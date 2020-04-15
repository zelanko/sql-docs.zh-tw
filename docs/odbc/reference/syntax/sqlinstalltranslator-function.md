---
title: SQL安裝翻譯功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300318"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函式
**一致性**  
 版本介紹: ODBC 2.5, 已棄用  
  
 **摘要**  
 在 ODBC 3.0 中 **,SQLInstall 轉換器**已被[SQLInstall 翻譯器所取代](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 對**SQLInstall 翻譯器的**呼叫將映射到**SQLInstall 翻譯器Ex**。 有關詳細資訊,請參閱**SQLInstall 翻譯器Ex**。  
  
 如果應用程式在 ODBC *3.x*驅動程式管理員中呼叫它 *,lpszInfFile*參數設定為 NULL 以外的值 **,SQLInstall 轉換器**將返回 FALSE。 ODBC *2.x*中使用的 Odbc.inf 檔在 ODBC *3.x*中不再受支援,即使對於向後相容性也是如此。
