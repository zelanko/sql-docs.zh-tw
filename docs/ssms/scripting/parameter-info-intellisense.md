---
title: 參數資訊 (IntelliSense)
description: 了解如何使用 IntelliSense [參數資訊] 選項，其會在鍵入函式或預存程序所需的參數時，提供相關資訊。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cbd2f430583b125333f11184bf49d86fafdb8ae1
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901741"
---
# <a name="parameter-info-intellisense"></a>參數資訊 (IntelliSense)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 的 [參數資訊]**** 選項會開啟一個參數清單，為您提供函數或預存程序所需之參數數目、名稱和類型的相關資訊。 粗體的參數表示當您輸入函數或預存程序時所需的下一個參數。  
  
 巢狀函數也有參數清單。 如果您將函數當作參數輸入到另一個函數中，參數清單會顯示內部函數的參數。 之後，當內部函數參數清單完成時，參數清單會回復成顯示外部函數參數。  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>檢視函數或預存程序的參數資訊  
  
1.  在函數名稱之後，依照通常開啟參數清單時的相同輸入方式，輸入一個左括號。 輸入預存程序的名稱之後，以您通常輸入的方式輸入一個空格，即可取得有關程序參數的資訊。  
  
     此時 IntelliSense 會在插入點之下，在快顯視窗中，顯示函數的完整宣告或預存程序的參數。 清單中的第一個參數會以粗體字顯示。  
  
2.  當您輸入參數時，會變更粗體字型來反映您必須輸入的下一個參數。  
  
3.  您隨時可以按 ESC 來關閉這份清單，或繼續輸入直到函數完成。  
  
     如果是函數，當您輸入右括號時，也會關閉參數清單。  
  
#### <a name="to-manually-start-parameter-info"></a>手動啟動參數資訊  
  
1.  按一下 [編輯] 功能表，選取 [IntelliSense]，然後選取 [參數資訊]。  
  
2.  按下 CTRL+SHIFT+SPACE 鍵盤快速鍵。  
  
 如需詳細資訊，請參閱[設定 IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md)。  
  
> [!NOTE]  
>  [參數資訊] 選項僅適用於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器和 XML 查詢編輯器。  
  
  
