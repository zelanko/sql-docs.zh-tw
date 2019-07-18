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
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125731"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC *2.x*應用程式會呼叫**SQLInstallTranslator**透過 ODBC *3.x*驅動程式，驅動程式管理員會對應到呼叫**SQLInstallTranslatorEx**。應用程式不應該呼叫**SQLInstallTranslator**在 ODBC *3.x*使用的驅動程式管理員*lpszInfFile*引數設定為 NULL 以外的值。 ODBC。在 ODBC 中使用的 INF 檔案*2.x*不再支援 ODBC *3.x*、 甚至是為了與舊版相容。
