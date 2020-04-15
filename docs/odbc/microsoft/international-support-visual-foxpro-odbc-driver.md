---
title: 國際支援(視覺福克斯Pro ODBC驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299968"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>國際支援 (Visual FoxPro ODBC Driver)
微軟視覺化福斯Pro ODBC驅動程式支援:  
  
-   雙位元組數集 (DBCS)  
  
-   多個整理序列  
  
 整理序列定義儲存在 Visual FoxPro 表或資料庫中的*排序順序*。 預設情況下,驅動程式配置為使用支援作業系統語言版本的整理序列。  
  
 有關支援的整理序列的清單,請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>地區設定  
 對應於給定語言和國家/地區的資訊集。 區域設置指示特定的設置,如十進位隔元、日期和時間格式以及字元排序順序。  
  
## <a name="sort-order"></a>排序次序 (sort order)  
 排序順序包含不同*區域設定*的排序規則,允許您正確排序這些語言中的數據。 在 Visual FoxPro 中,當前排序順序確定字元表達式比較的結果以及記錄在索引表或排序表中的顯示順序。
