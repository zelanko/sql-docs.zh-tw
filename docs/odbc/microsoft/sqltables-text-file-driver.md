---
description: SQLTables (文字檔驅動程式)
title: SQLTables (文字檔驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6c6f65603cee70811d7c9894ba9d840d28ad4f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339667"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*唯一有效的引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當 *szTableOwner* 設定為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中會傳回 Null。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 資料行中， **SQLTables** 會傳回目錄的路徑。|  
|*SzTableType*|「資料表」是唯一支援的資料表類型。<br /><br /> 使用文字驅動程式時， **SQLTables**傳回的檔案清單是由 [ **ODBC 文字設定**] 對話方塊之 [延伸模組]**清單**框中的副檔名所決定。|
