---
title: "REPLACENULL (SSIS 運算式) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# REPLACENULL (SSIS 運算式)
  如果第一個運算式參數的值為 NULL，則會傳回第二個運算式參數的值，否則會傳回第一個運算式的值。  
  
## 語法  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## 引數  
 *運算式 1*  
 檢查此運算式的結果是否為 NULL。  
  
 *運算式 2*  
 如果第一個運算式評估為 NULL，則傳回此運算式的結果。  
  
## 結果類型  
 DT_WSTR  
  
## 備註  
  
-   *expression 2* 的長度可以為零。  
  
-   如果任何引數為 Null，則 REPLACENULL 會傳回 Null 結果。  
  
-   任一參數都不支援 BLOB 資料行 (DT_TEXT、DT_NTEXT、DT_IMAGE)。  
  
-   兩個運算式應該有相同的傳回類型。 如果不相同，則函式嘗試將第二個運算式轉換成第一個運算式的傳回類型，如果資料類型不相容，這可能會導致錯誤。  
  
## 運算式範例  
 下列範例會將資料庫資料行中的任何 NULL 值取代成字串 (1900-01-01)。 在您要將 NULL 值取代成其他任何值的通用衍生資料行圖樣中，特別會使用此函式。  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]  
>  下列範例會示範 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 的作法。  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? “1900-01-01” : MyColumn)   
```  
  
  