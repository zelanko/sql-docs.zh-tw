---
title: 國際支援（Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: e987c224f2d716fcab3bf898b1cb276e922e48ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085497"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>國際支援 (Visual FoxPro ODBC Driver)
Microsoft Visual FoxPro ODBC 驅動程式支援：  
  
-   雙位元組字集（DBCS）  
  
-   多個排序次序  
  
 排序次序會定義儲存在 Visual FoxPro 資料表或資料庫中的資料*排序次序*。 根據預設，驅動程式會設定為使用支援作業系統語言版本的定序序列。  
  
 如需支援的定序序列清單，請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>地區設定  
 對應至指定語言和國家/地區的資訊集。 地區設定會指出特定的設定，例如小數分隔符號、日期和時間格式，以及字元排序次序。  
  
## <a name="sort-order"></a>排序次序 (sort order)  
 排序次序會併入不同*地區*設定的排序規則，讓您能夠正確地排序這些語言的資料。 在 Visual FoxPro 中，目前的排序次序會決定字元運算式比較的結果，以及記錄在索引或已排序資料表中的顯示順序。
