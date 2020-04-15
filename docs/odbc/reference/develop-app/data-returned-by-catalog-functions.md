---
title: 目錄函數傳回的資料 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305224"
---
# <a name="data-returned-by-catalog-functions"></a>目錄函式所傳回的資料
每個目錄函數作為結果集返回數據。 此結果集與任何其他結果集沒有什麼不同。 它通常由預定義的參數化**SELECT**語句生成,該語句在驅動程式中硬編碼或存儲在數據源中的一個過程中。 有關如何從結果集中檢索數據的資訊,請參閱["已創建結果集?"。](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
 每個目錄函數的結果集在該函數的引用條目中描述。 除了列出的列外,結果集還可以包含最後一個預定義列之後的特定於驅動程式的列。 驅動程序文件中描述了這些列(如果有)。  
  
 應用程式應綁定相對於結果集末尾的特定於驅動程式的列。 也就是說,它們應計算特定於驅動程式的列的數量,因為最後一列的編號 (使用**SQLNumResultCols**檢索 ) 減去在所需列之後發生的列數。 這樣,當在 ODBC 或驅動程式的未來版本中將新列添加到結果集時,無需更改應用程式。 要使此方案正常工作,驅動程式必須在舊特定於驅動程式的列之前添加新的特定於驅動程式的列,以便列號不會相對於結果集的末尾更改。  
  
 在結果集中返回的標識碼不會引用,即使它們包含特殊字元。 例如,假設標識符報價字元(特定於驅動程式並通過**SQLGetInfo**返回)是一個雙引號 ("),並且應付帳款表包含名為「客戶名稱」的列。 在**SQLColumn**為此列返回的行中,TABLE_NAME列的值是應付帳款,而不是"應付帳款",COLUMN_NAME列的值是客戶名稱,而不是"客戶名稱」。 若要檢查的客戶名稱,應用程式將參考以下名稱:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 有關詳細資訊,請參考[識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目錄函數基於類似 SQL 的授權模型,其中基於使用者名和密碼建立連接,並且僅返回使用者具有許可權的數據。 單個檔的密碼保護(不適合此模型)是驅動程式定義的。  
  
 目錄函數返回的結果集幾乎永遠不會升級,應用程式不應期望通過更改這些結果集中的數據來更改資料庫的結構。
