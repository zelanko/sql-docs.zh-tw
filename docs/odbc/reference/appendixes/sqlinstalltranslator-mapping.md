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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300580"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC 2.x*應用程式**透過 odbc 3.x*驅動程式呼叫**SQLInstallTranslator**時，驅動程式管理員會將呼叫對應至**SQLInstallTranslatorEx**。應用程式不應該*在 ODBC 3.X*驅動程式管理員中呼叫**SQLInstallTranslator** ，並將*LPSZINFFILE*引數設定為 Null 以外的值。 ODBC。*Odbc 3.x 中已不再*支援用於 odbc 2.X 的 INF*檔案，即使*是回溯相容性也一樣。
