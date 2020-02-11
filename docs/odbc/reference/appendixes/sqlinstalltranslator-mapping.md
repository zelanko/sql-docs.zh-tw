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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125731"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 對應
當 ODBC 2.x*應用程式**透過 odbc 3.x*驅動程式呼叫**SQLInstallTranslator**時，驅動程式管理員會將呼叫對應至**SQLInstallTranslatorEx**。應用程式不應該*在 ODBC 3.X*驅動程式管理員中呼叫**SQLInstallTranslator** ，並將*LPSZINFFILE*引數設定為 Null 以外的值。 ODBC。*Odbc 3.x 中已不再*支援用於 odbc 2.X 的 INF*檔案，即使*是回溯相容性也一樣。
