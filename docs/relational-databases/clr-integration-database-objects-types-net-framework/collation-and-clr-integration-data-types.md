---
title: 排序與 CLR 的資料型態 :微軟文件
description: 在 SQL Server CLR 整合中,.NET 框架字串 API 使用目前的線程的「文化資訊」的 CompareInfo 屬性執行字串比較。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: 46e4d450db90e4bfc93187a48ca8adae472036c6
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488483"
---
# <a name="collation-and-clr-integration-data-types"></a>定序和 CLR 整合資料類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]中,**比較資訊**物件處理排序規則。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字串應用程式編程介面 (API) 使用與目前的線程的**區域性資訊**物件關聯的**CompareInfo**屬性執行字串比較。 **區域性資訊**物件的預設設置基於正在運行的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算機 的 Windows 區域設置。 這將確定預設比較語義(如果未指定顯式**區域性資訊**)用於**比較 System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會顯式將**CompareInfo**屬性更改為資料庫或伺服器排序規則。 如果需要,用戶必須在其例程中設置相應的**比較資訊**屬性。  
  
## <a name="parameter-collation"></a>參數定序  
 當您創建通用語言運行時 (CLR) 例程時,綁定到例程的 CLR 方法的參數是**SQLString**類型,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]創建參數的實例,其中包含調用例程的資料庫的預設排序。 如果參數不是**SqlType(** 例如,**字串**而不是**SQLString),** 則資料庫中的排序規則資訊不與參數相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
