---
title: "SQLInstallTranslator 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07308a2c737f2fbe6857d8a65a913f881b8e658f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC 2。*x*應用程式會呼叫**SQLInstallTranslator**透過 ODBC 3*.x*驅動程式，驅動程式管理員會將對應的呼叫**SQLInstallTranslatorEx**.應用程式不應該呼叫**SQLInstallTranslator**在 ODBC 3*.x*驅動程式管理員與*lpszInfFile*引數設定為 NULL 以外的值。 ODBC。ODBC 2 中使用的 INF 檔案。*x*已不再支援在 ODBC 3*.x*即使回溯相容性。

