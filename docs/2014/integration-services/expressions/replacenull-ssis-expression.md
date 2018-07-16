---
title: REPLACENULL (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab1f7be1f763dbb405d5c65d29c25381e0c09d2e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330038"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (SSIS 運算式)
  如果第一個運算式參數的值為 NULL，則會傳回第二個運算式參數的值，否則會傳回第一個運算式的值。  
  
## <a name="syntax"></a>語法  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>引數  
 *運算式 1*  
 檢查此運算式的結果是否為 NULL。  
  
 *運算式 2*  
 如果第一個運算式評估為 NULL，則傳回此運算式的結果。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
  
-   *expression 2* 的長度可以為零。  
  
-   如果任何引數為 Null，則 REPLACENULL 會傳回 Null 結果。  
  
-   任一參數都不支援 BLOB 資料行 (DT_TEXT、DT_NTEXT、DT_IMAGE)。  
  
-   兩個運算式應該有相同的傳回類型。 如果不相同，則函式嘗試將第二個運算式轉換成第一個運算式的傳回類型，如果資料類型不相容，這可能會導致錯誤。  
  
## <a name="expression-examples"></a>運算式範例  
 下列範例會將資料庫資料行中的任何 NULL 值取代成字串 (1900-01-01)。 在您要將 NULL 值取代成其他任何值的通用衍生資料行圖樣中，特別會使用此函式。  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]  
>  下列範例會示範 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]的作法。  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? “1900-01-01” : MyColumn)   
```  
  
  
