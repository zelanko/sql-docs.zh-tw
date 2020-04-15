---
title: 基於檔案的驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306661"
---
# <a name="file-based-drivers"></a>以檔案為基礎的驅動程式
基於文件的驅動程式與數據來源(如 dBASE)一起使用,這些數據來源不提供獨立資料庫引擎供驅動程式使用。 這些驅動程式直接存取實體資料,並且必須實現資料庫引擎來處理 SQL 語句。 作為一種標準做法,基於檔的驅動程式中的資料庫引擎實現由最低 SQL 一致性級別定義的 ODBC SQL 子集;有關此一致性等級的 SQL 語句的清單,請參閱附錄[C:SQL 語法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比較基於檔的驅動程式和基於 DBMS 的驅動程式時,基於檔的驅動程式更難編寫,因為資料庫引擎元件,配置起來不太複雜,因為沒有網路部分,而且功能較弱,因為很少有人有時間編寫資料庫引擎,就像資料庫公司生成的引擎那樣強大。  
  
 下圖顯示了基於檔的驅動程式的兩種不同的配置,一種是數據駐留在本地,另一種位於網路文件伺服器上。  
  
 ![基於&#45;驅動程式的兩種設定](../../odbc/reference/media/pr06.gif "pr06")
