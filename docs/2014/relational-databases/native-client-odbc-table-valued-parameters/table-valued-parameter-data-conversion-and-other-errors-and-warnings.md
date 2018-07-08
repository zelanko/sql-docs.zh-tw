---
title: 資料表值參數資料轉換和其他錯誤和警告 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8506311d0d95ac9d0f8eedc7632379b6bd9ce0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431867"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>資料表值參數資料轉換及其他錯誤和警告
  資料表值參數資料行值可以在用戶端和伺服器資料類型之間轉換，其轉換方式與其他資料行和參數值相同。 因為資料表值參數可以包含多個資料行和多個資料列，所以能夠識別發生錯誤的實際值是很重要的一件事。  
  
 當資料表值參數資料行中偵測到錯誤或警告時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 將會產生診斷記錄。 錯誤訊息將會包含資料表值參數的參數編號，加上資料行序數和資料列號碼。 應用程式可以使用診斷記錄中的診斷欄位 SQL_DIAG_SS_TABLE_COLUMN_NUMBER 和 SQL_DIAG_SS_TABLE_ROW_NUMBER，以判斷哪些值與錯誤和警告有關。 這些診斷欄位會在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中提供。  
  
 診斷記錄的 SQLSTATE 和訊息元件將會在所有其他層面符合現有的 ODBC 行為。 也就是說，除了參數、資料列和資料行識別資訊以外，錯誤訊息的資料表值參數值會與非資料表值參數的值相同。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
