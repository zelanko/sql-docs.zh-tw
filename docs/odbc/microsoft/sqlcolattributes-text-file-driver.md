---
description: SQLColAttributes (文字檔驅動程式)
title: SQLColAttributes (文字檔驅動程式) |Microsoft Docs
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
ms.openlocfilehash: ee659f984f75b3ede7fc09e698e58b427158f9fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412204"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|屬性|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|針對 LONGVARBINARY 資料，SQL_COLUMN_DISPLAY_SIZE 是資料行的最大長度，而不是資料行次的最大長度2。|  
|SQL_OWNER_NAME|因為不支援擁有者名稱，所以在此資料行中會傳回空字串 ( "" ) 。|  
|SQL_QUALIFIER_NAME|傳回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|系統會將 LONGVARBINARY 和 LONGVARCHAR 資料行回報為 SQL_UNSEARCHABLE。<br /><br /> 即使 LONGVARBINARY 和 LONGVARCHAR 不是，固定長度和可變長度的二進位和字元資料類型都是可搜尋的。|
