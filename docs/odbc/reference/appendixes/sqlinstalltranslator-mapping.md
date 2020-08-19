---
description: SQLInstallTranslator 對應
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc571e305070e4afba6dc7c647d18a6790c011f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448967"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC 2.x*應用程式**透過 odbc 3.x*驅動程式呼叫**SQLInstallTranslator**時，驅動程式管理員會將呼叫對應至**SQLInstallTranslatorEx**。應用程式不應*呼叫 ODBC 3.X*驅動程式管理員中的**SQLInstallTranslator** ，並將*LPSZINFFILE*引數設定為 Null 以外的值。 ODBC。Odbc 2.x 中使用的 INF *檔案已不再* 受到 odbc *3.x 的支援，即使*是回溯相容性也是如此。
