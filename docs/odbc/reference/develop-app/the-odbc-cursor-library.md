---
title: "ODBC 資料指標程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6250d693414a9d63077bcc5e47438d847ae72ce
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="the-odbc-cursor-library"></a>ODBC 資料指標程式庫
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 區塊和可捲動資料指標是許多應用程式非常有用的新增項目。 不過，並非所有的驅動程式所支援的區塊和可捲動資料指標。 相同為 true 的定位更新及刪除陳述式和**SQLSetPos**，更新資料中會討論。 因此，ODBC SDK 元件的 Windows，先前包含在 Microsoft 資料存取元件 (MDAC) SDK，包含資料指標程式庫。 資料指標程式庫實作區塊、 靜態資料指標、 定位的 update 和 delete 陳述式，和**SQLSetPos**符合開啟群組標準 CLI 一致性層級的任何驅動程式。 資料指標程式庫可能與 ODBC 應用程式一起轉散發授權合約中的 SDK 的詳細資訊，請參閱。  
  
 若要使用資料指標程式庫，應用程式才能連線到資料來源設定 SQL_ATTR_ODBC_CURSORS 連接屬性。 如需有關資料指標程式庫的詳細資訊，請參閱[附錄 f: ODBC 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
