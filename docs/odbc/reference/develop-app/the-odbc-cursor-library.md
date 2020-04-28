---
title: ODBC 資料指標程式庫 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300048"
---
# <a name="the-odbc-cursor-library"></a>ODBC 資料指標程式庫
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 區塊和可滾動的資料指標對許多應用程式而言都是非常有用的新增功能。 不過，並非所有的驅動程式都支援區塊和可滾動的資料指標。 定位 update 和 delete 語句和**SQLSetPos**也是如此，這會在更新資料中討論。 因此，先前包含在 Microsoft Data Access Components （MDAC） SDK 中的 Windows SDK ODBC 元件包含資料指標程式庫。 資料指標程式庫會針對任何符合開放式群組標準 CLI 一致性層級的驅動程式，執行區塊、靜態資料指標、定點更新和刪除語句，以及**SQLSetPos** 。 資料指標程式庫可以與 ODBC 應用程式一起轉散發;如需詳細資訊，請參閱 SDK 中的授權合約。  
  
 若要使用資料指標程式庫，應用程式會先設定 SQL_ATTR_ODBC_CURSORS 連接屬性，再將它連接至資料來源。 如需資料指標程式庫的詳細資訊，請參閱[附錄 F： ODBC 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
