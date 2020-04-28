---
title: SQLColAttributes （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eafe02ba76dcaa6078abee862d743deb4765bdd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307919"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|屬性|評價|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|若為 LONGVARBINARY 資料，SQL_COLUMN_DISPLAY_SIZE 是資料行的最大長度，而不是資料行次的最大長度2。|  
|SQL_OWNER_NAME|此資料行中會傳回空字串（""），因為不支援擁有者名稱。|  
|SQL_QUALIFIER_NAME|會傳回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 資料行會回報為 SQL_UNSEARCHABLE。<br /><br /> 固定長度和可變長度的二進位和字元資料類型是可搜尋的，即使 LONGVARBINARY 和 LONGVARCHAR 不是也一樣。|
