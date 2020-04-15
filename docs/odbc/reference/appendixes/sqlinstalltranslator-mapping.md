---
title: SQL安裝轉換器映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300580"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC *2.x*應用程式透過 ODBC *3.x*驅動程式呼叫**SQLInstall 轉換器**時,驅動程式管理員將呼叫映射到**SQLInstall 翻譯器Ex**。應用程式不應在 ODBC *3.x*驅動程式管理員中呼叫**SQLInstall 轉換器***,lpszInfFile*參數設定為 NULL 以外的值。 ODBC。ODBC *2.x*中使用的 INF 檔在 ODBC *3.x*中不再受支援,即使對於向後相容性也是如此。
