---
description: SQLGetConnectOption (Visual FoxPro ODBC Driver)
title: SQLGetConnectOption (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd22ec3862ff2f0f3c4f7b5aa9dbeff53a5d8cfe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411784"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援：部分  
  
 ODBC API 一致性：層級1  
  
 傳回連接選項的目前設定。 此為部分支援的函式：驅動程式支援*fOption*引數的所有值，但不支援*fOption*引數 SQL_TXN_ISOLATION 的部分*vParam*值。  
  
 下表僅描述具有 **SQLGetConnectOption**之 VISUAL FoxPro ODBC 驅動程式執行特定行為的引數。  
  
|*fOption*|備註|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF，則您的應用程式必須使用 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)明確認可或復原交易;Visual FoxPro ODBC 驅動程式不會在完成時自動認可哥交易語句。 如果可交易語句，驅動程式就會開始交易。|  
|SQL_CURRENT_QUALIFIER|可以是完整的資料庫 (. dbc 檔案) 名稱或目錄的完整路徑，該目錄包含零或多個資料表 ( .dbf 檔案) 。|  
|SQL_LOGINTIMEOUT|傳回「驅動程式無法支援」錯誤。|  
|SQL_CURSORS|傳回「驅動程式無法支援」錯誤。|  
|SQL_PACKET_SIZE|傳回「驅動程式無法支援」錯誤。|  
|SQL_TXN_ISOLATION|驅動程式只允許 SQL_TXN_READ_COMMITTED。<br /><br /> 不支援下列 *vParam*：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) 。
