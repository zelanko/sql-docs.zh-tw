---
title: ODBC 游標庫 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300048"
---
# <a name="the-odbc-cursor-library"></a>ODBC 資料指標程式庫
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 塊和可滾動遊標是許多應用程式的非常有用的附加功能。 但是,並非所有驅動程式都支持塊和可滾動的游標。 定位更新和刪除語句和**SQLSetPos**也是如此,在更新數據中討論。 因此,以前包含在 Microsoft 資料存取元件 (MDAC) SDK 中的 Windows SDK 的 ODBC 元件包括游標庫。 游標庫為滿足開放組標準 CLI 一致性級別的任何驅動程式實現塊、靜態游標、定位更新和刪除語句以及**SQLSetPos。** 游標庫可以與 ODBC 應用程式重新分發;有關詳細資訊,請參閱 SDK 中的許可協定。  
  
 要使用游標庫,應用程式在連接到數據源之前設置SQL_ATTR_ODBC_CURSORS連接屬性。 有關游標庫的詳細資訊,請參閱附錄[F:ODBC 游標庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
