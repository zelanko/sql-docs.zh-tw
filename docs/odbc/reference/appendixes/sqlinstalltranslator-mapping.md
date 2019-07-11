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
ms.openlocfilehash: 50bfa00f482110d3d0695ef249e8758b5db02c80
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792799"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC *2.x*應用程式會呼叫**SQLInstallTranslator**透過 ODBC *3.x*驅動程式，驅動程式管理員會對應到呼叫**SQLInstallTranslatorEx**。應用程式不應該呼叫**SQLInstallTranslator**在 ODBC *3.x*使用的驅動程式管理員*lpszInfFile*引數設定為 NULL 以外的值。 ODBC。在 ODBC 中使用的 INF 檔案*2.x*不再支援 ODBC *3.x*、 甚至是為了與舊版相容。
