---
description: SQLTables (dBASE 驅動程式)
title: SQLTables (dBASE 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cadded2fe1dfdcb99902a69bb5cbc0608b4614e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339894"
---
# <a name="sqltables-dbase-driver"></a>SQLTables (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*唯一有效的引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當 *szTableOwner* 設定為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中會傳回 Null。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 資料行中， **SQLTables** 會傳回目錄的路徑。|  
|*SzTableType*|針對 dBASE 檔案，「資料表」是唯一支援的資料表類型。|
