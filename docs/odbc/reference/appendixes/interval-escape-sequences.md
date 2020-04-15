---
title: 間隔轉義序列 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304953"
---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 使用轉義序列進行間隔文字。 此逸出序列的語法如下:  
  
 【*間隔文字*】  
  
 有關*間隔文本*的 BNF 語法,請參閱本附錄後面的[間隔文本語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)部分。  
  
 如果資料來源支援間隔資料類型,則支援間隔文字轉義序列。 應用程式應呼叫**SQLGetTypeInfo**以確定是否支援這些資料類型。
