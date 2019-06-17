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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a85868cf22fa6d385c3bf75261e0f1cd54e4e1d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149072"
---
# <a name="the-odbc-cursor-library"></a>ODBC 資料指標程式庫
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 區塊及可捲動資料指標會非常有用的新功能，對許多應用程式。 不過，並非所有的驅動程式支援區塊和可捲動資料指標。 相同成立的定位的 update 和 delete 陳述式及**SQLSetPos**，其中會討論更新資料的資料。 因此，ODBC 元件的 Windows sdk，原本是收錄在 Microsoft Data Access Components (MDAC) SDK，包括資料指標程式庫。 資料指標程式庫實作區塊、 靜態資料指標、 定位的 update 和 delete 陳述式，並**SQLSetPos**符合開啟群組的標準 CLI 一致性層級的任何驅動程式。 資料指標程式庫可轉散發 ODBC 應用程式;授權協議中的 SDK，如需詳細資訊，請參閱。  
  
 若要使用資料指標程式庫，應用程式會設定 SQL_ATTR_ODBC_CURSORS 連接屬性，才能連線到資料來源。 如需有關資料指標程式庫的詳細資訊，請參閱[附錄 f:ODBC 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
