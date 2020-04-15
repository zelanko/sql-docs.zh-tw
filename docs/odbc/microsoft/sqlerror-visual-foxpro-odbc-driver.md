---
title: SQLError(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298678"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 返回有關上次錯誤的錯誤或狀態資訊。 驅動程式維護一個堆疊或錯誤列表,這些錯誤可以返回*用於 hstmt、hdbc*和*henv*參數,具體取決於對**SQLError**的調用方式。 *hdbc* 在每個語句之後刷新錯誤佇列。  
  
 下表描述了驅動程式使用的**SQLError**參數和返回值。  
  
|SQLError 參數|傳回值描述|  
|-----------------------|------------------------------|  
|*szSQL國家*|由錯誤表示的 SQLSTATE 的值。|  
|*pfNativeError*|非零值表示視覺[FoxPro ODBC 驅動程式本機錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值為零表示驅動程式偵測到錯誤並映射到相應的[ODBC 錯誤程式](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*什洛姆斯格*|這個機錯誤或 ODBC 錯誤的文字。|  
|*多加錯姆斯格*|消息文本的長度加上標識符的長度。|  
  
 關於驅動程式錯誤訊息的詳細資訊,請參考[錯誤訊息摘要](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 有關此功能的詳細資訊,請參閱*ODBC 程式師參考*中的[SQLError。](../../odbc/reference/syntax/sqlerror-function.md)
