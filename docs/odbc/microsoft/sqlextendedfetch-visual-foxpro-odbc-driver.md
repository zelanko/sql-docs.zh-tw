---
title: SQLExtendedFetch （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4336f76093383a170fbb1028851564098213a74d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904543"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 2  
  
 類似於[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)但傳回每個資料行使用陣列的多個資料列。 結果集是順向可捲動且可進行回溯可捲動資料指標定義為靜態，不是順如果。  
  
 根據預設，Visual FoxPro ODBC 驅動程式不會傳回資料列標示為 FoxPro 資料表中刪除。 標示為刪除但尚未從資料表移除資料列不會包含在結果集資料指標。 您可以使用來變更此行為[設定刪除](../../odbc/microsoft/set-deleted-command.md)命令。  
  
 如需詳細資訊，請參閱[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)中*ODBC 程式設計人員參考*。
