---
title: SQLInstallTranslator 對應 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9760bfad769e9508d58d1cd00f98376dbd13d877
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298513"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC 2。*x*應用程式會呼叫**SQLInstallTranslator**透過 ODBC 3 *.x*驅動程式，驅動程式管理員會對應到呼叫**SQLInstallTranslatorEx**.應用程式不應該呼叫**SQLInstallTranslator**在 ODBC 3 *.x*使用的驅動程式管理員*lpszInfFile*引數設定為 NULL 以外的值。 ODBC。ODBC 2 中所使用的 INF 檔案。*x*不再支援在 ODBC 3 *.x*、 甚至是為了與舊版相容。
