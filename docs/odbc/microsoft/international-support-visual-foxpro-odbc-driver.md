---
title: 國際支援 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50d65520e74a4e11bada88795fedc0b2f2e82628
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853096"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>國際支援 (Visual FoxPro ODBC Driver)
Microsoft Visual FoxPro ODBC Driver 支援：  
  
-   雙位元組字元集 (DBCS)  
  
-   多個定序順序  
  
 定序的順序會定義*排序次序*Visual FoxPro 資料表或資料庫中儲存的資料。 根據預設，此驅動程式被設定為使用支援您的作業系統的語言版本的定序序列。  
  
 如需支援的定序順序的清單，請參閱 <<c0> [ 設定定序](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>地區設定 (locale)  
 對應至指定的語言和國家/地區的資訊集。 地區設定會指出特定的設定，例如小數分隔符號，日期和時間格式字元排序順序。  
  
## <a name="sort-order"></a>排序次序 (sort order)  
 排序次序納入不同的排序規則*地區設定*s，可讓您正確地排序這些語言中的資料。 Visual FoxPro，在目前的排序順序會決定結果的字元運算式比較和記錄出現在中編製索引，或排序資料表的順序。
