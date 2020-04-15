---
title: 手動提交模式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287872"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動提交模式下,* 應用程式必須通過調用**SQLEndTran**來顯式完成事務,以提交它們或回滾它們。 這是大多數關係資料庫的正常事務模式。  
  
 ODBC 中的事務不必顯式啟動。 相反,每當應用程式開始在資料庫上運行時,事務都會隱式啟動。 如果數據源需要顯式事務啟動,則每當應用程式執行需要事務的語句並且沒有當前事務時,驅動程式必須提供它。
