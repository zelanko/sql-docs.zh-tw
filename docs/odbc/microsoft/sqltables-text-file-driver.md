---
title: SQLTables （文字檔驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fcdf9cc41a55d1e529001ae7183ef9fa833363b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949019"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|唯一有效的引數，如*szTableOwner*是 NULL，因為沒有任何驅動程式支援擁有者名稱。 具有*szTableOwner*設為 NULL，會傳回所有資料表。 TABLE_OWNER 資料行就會傳回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 欄中， **SQLTables**會傳回目錄的路徑。|  
|*SzTableType*|「 資料表 」 是唯一支援的資料表類型。<br /><br /> 文字驅動程式使用時，所傳回的檔案清單**SQLTables**取決於中的檔案副檔名**延伸模組清單**方塊中**ODBC 文字設定** 對話方塊。|
