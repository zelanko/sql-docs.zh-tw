---
title: SQLNativeSql(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300568"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLNativeSql**函數。 有關**SQLNativeSql**的一般資訊,請參閱[SQLNativeSql 函數](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驅動程式支援此功能,游標庫將在驅動程式中調用**SQLNativeSql**並將其傳遞給 SQL 語句。 對於定位更新、定位刪除和**選擇更新**語句,游標庫在將語句傳遞給驅動程式之前修改該語句。  
  
> [!NOTE]  
>  如果游標名稱在**SQLNativeSql**的*InofText*參數中傳遞的定位更新或刪除語句中無效,則游標庫錯誤地返回 SQLSTATE 34000(無效游標名稱)。 **SQLNativeSql**不打算返回語法錯誤,這些錯誤僅在語句準備或執行時返回。
